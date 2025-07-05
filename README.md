# Kubernetes Containerisation - Basic Setup

This guide explains how to set up **Minikube** and **kubectl** for Kubernetes containerisation using **WSL (Windows Subsystem for Linux)** on a Windows machine.

---

##  Requirements

- Windows with WSL enabled
- Docker Desktop (with WSL integration)
- WSL distro (e.g., Ubuntu)

---

##  Step-by-Step Installation

### 🔹 1. Install `kubectl` on Windows (via Chocolatey)

Open **Command Prompt as Administrator** and run:

```powershell
choco install kubernetes-cli
```
In order to install brew
```powershell
https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Install minikube using brew
```powershell
brew install minikube
```
Start the minikube using docker
```powershell
minikube start --driver=docker
```
Gives the status of minikube 
```powershell
minikube status
```
Provides the ip address of minikube at which its running 
```powershell
minikube ip 
```
Opening the shell so u can interacte with the cluster .
```powershell
minikube ssh
```
This opens a shell u can exiting by the command 
```powershell
exit
```
Control Plane is running at ip address
```powershell
kubectl cluster-info
```
To fetch pods
```powershell
kubectl get pods
```
To fetch namespaces at which pods are there
```powershell
kubectl get namespaces
```
create pod named nginx inside docker image
```powershell
kubectl run nginx --image=nginx
```
describe the pod nginx
it displays ip address of node (Node: minikube/192.168.49.2)
```powershell
kubectl desctibe pod nginx
```
displays all the current docker containers running on ur system
```powershell
minikube ps
```
index.mjs file is used because import statement is used instead of required statement


 in the dokcer file we have 
 from node: alpine
 expose port 3000
 copy package.json and package-lock.json
 then run npm install
 this file will be copied to the app folder inside of the image
 copy all remainig files to app folder
 then npm start instruction is run
alias k="kubectl"
kubectl get pod
kubectl get nodes
k get deploy
kubectl describe pod k8s-web-hello
docker build . -t arjunsreekumar/k8s-web-hello
docker login
docker pull <podname>
k rollout restart deployment
minikube service k8s-web-hello
 rolling update means if new bods r gone they are replaced with new ones-- if u del old pod new replaces
kubectl set image deployment k8s-web-hello k8-web-hello=arjunsreekumar/k8-web-hello:3.0.0 this can be used to rollout
kubectl rollout undo deployment k8s-web-hello can be used to rollback
minikube dashboard

kubectl delete all --all
deletes the kubernetes service as well but is recreated after it
Mi in memory means megabytes
cpu 500 m means half of capability



docker push arjunsreekumar/k8s-web-to-nginx:v11
kubectl set image deployment/k8s-web-to-nginx k8s-web-to-nginx=arjunsreekumar/k8s-web-to-nginx:v11
kubectl rollout status deployment/k8s-web-to-nginx
kubectl rollout restart deployment k8s-web-to-nginx
minikube service k8s-web-to-nginx
