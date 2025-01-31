# Prometheus / Grafana Monitoring for KIND Cluster

### Pre-Requisites:-
1. Linux system (Ubuntu/I'm using WSL for Windows)
2. 8GB Ram & 100GB Storage
3. Docker to be Installed

<br>
KIND is a tool for running local Kubernetes clusters using Docker container “nodes”.
KIND was primarily designed for testing Kubernetes itself, but may be used for local development or CI.
<br><br>

### KIND Installation:-
```
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.26.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/
```
Pull the node image:-
```
docker pull kindest/node:v1.32.0
```

<br>

Create KIND Cluster with name 'pga':-
```
kind create cluster --name pga
```
<img width="781" alt="image" src="https://github.com/user-attachments/assets/9f02c199-4731-4dff-9277-2d4fe843a239" />'

<br>

### Helm Install
Helm is a tool for managing Kubernetes applications. It's an open-source package manager that uses YAML-based "charts" to streamline the deployment and management of applications. 
```
sudo snap install helm --classic
```

<br>
============================================================================================

<br>

### Deploying Prometheus using helm charts
Now we will deploy Prometheus on a Kubernetes cluster using Helm charts:

Make sure that you have a kubernetes cluster is already running.
1. Firstly, we will add the helm repository which is required
2. Update the repository
```
helm repo add stable https://charts.helm.sh/stable
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

<br>

<img width="818" alt="image" src="https://github.com/user-attachments/assets/2882a8d0-d211-418b-b4a5-5a8447a86c44" />'

<br>

Let’s install the Prometheus chart. You can find more details about this chart -
```
helm install prometheus prometheus-community/kube-prometheus-stack
```
<br>

<img width="944" alt="image" src="https://github.com/user-attachments/assets/ca77824e-4084-4a26-ad36-afb22f9dc41b" />

<br>

This chart will install additional charts as well:

Node-exporter on all the three nodes which are in your cluster -
1. High Available Grafana
2. High Available Prometheus
3. High Available Alert Manager
4. Operator
5. Kube State Metrics

Now you have Prometheus installed with the bundle of components required to operate it on a Kubernetes environment.

Access the Prometheus url on the browser

Now lets verify our installation and try to access it on browser using port-forward
```
kubectl port-forward prometheus-prometheus-kube-prometheus-prometheus-0 8000:9090
```
