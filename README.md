# Prometheus / Grafana Monitoring for KIND Cluster

Pre-Requisites:-
1. Linux system (Ubuntu/I'm using WSL for Windows)
2. 8GB Ram & 100GB Storage
3. Docker to be Installed

<br>
KIND is a tool for running local Kubernetes clusters using Docker container “nodes”.
KIND was primarily designed for testing Kubernetes itself, but may be used for local development or CI.
<br><br>

KIND Installation:-
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
<img width="781" alt="image" src="https://github.com/user-attachments/assets/9f02c199-4731-4dff-9277-2d4fe843a239" />

<br>

Install helm repository to make things:-
```
sudo snap install helm --classic
```
