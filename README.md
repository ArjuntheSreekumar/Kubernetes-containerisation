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
