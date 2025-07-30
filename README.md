# ðŸš€ Kubernetes Containerisation - Basic Setup (Minikube on WSL)

This guide explains how to set up **Minikube** and **kubectl** for Kubernetes containerisation using **WSL (Windows Subsystem for Linux)** on a Windows machine.

---

## âœ… Requirements

- Windows with WSL enabled
- Docker Desktop (with WSL integration enabled)
- A WSL Linux distribution (e.g., Ubuntu)
- Chocolatey (on Windows) or Homebrew (on WSL)

---

## âš™ï¸ Step-by-Step Installation

### ðŸ”¹ 1. Install `kubectl` on Windows

Open **Command Prompt as Administrator** and run:

```powershell
choco install kubernetes-cli
```

---

### ðŸ”¹ 2. Install Homebrew (on WSL)

Run this in your WSL terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

### ðŸ”¹ 3. Install Minikube via Homebrew

```bash
brew install minikube
```

---

### ðŸ”¹ 4. Start Minikube Using Docker Driver

```bash
minikube start --driver=docker
```

---

### ðŸ”¹ 5. Useful Minikube Commands

| Command                         | Description                              |
|----------------------------------|------------------------------------------|
| `minikube status`              | Show current Minikube status             |
| `minikube ip`                  | Get the IP address of Minikube           |
| `minikube ssh`                 | Open shell inside Minikube VM            |
| `exit`                         | Exit the Minikube SSH shell              |
| `minikube ps`                  | Show current Docker containers running   |
| `minikube dashboard`           | Launch the Kubernetes dashboard          |

---

## ðŸ“¡ Interacting with the Cluster (kubectl)

```bash
kubectl cluster-info              # Control plane info
kubectl get pods                  # List pods
kubectl get namespaces            # List namespaces
kubectl run nginx --image=nginx   # Create a pod using the nginx image
kubectl describe pod nginx        # View details about the nginx pod
kubectl get nodes                 # List cluster nodes
kubectl get deploy                # List deployments
```

Alias for `kubectl` (optional):

```bash
alias k="kubectl"
```

---

## ðŸ³ Docker + Node App Container (index.mjs)

Because `import` is used instead of `require`, `index.mjs` is the entry point.

### Example Dockerfile

```Dockerfile
FROM node:alpine
EXPOSE 3000
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

---

## ðŸš€ Build, Push, and Deploy

### Step 1: Build and Push Image

```bash
docker build . -t arjunsreekumar/k8s-web-hello
docker login
docker push arjunsreekumar/k8s-web-hello
```

### Step 2: Deploy to Kubernetes

```bash
kubectl create deployment k8s-web-hello --image=arjunsreekumar/k8s-web-hello
```

### Step 3: Expose the Service

```bash
kubectl expose deployment k8s-web-hello --type=NodePort --port=3000
minikube service k8s-web-hello
```

---

## ðŸ” Rolling Updates and Rollbacks

### Rolling Update

```bash
kubectl set image deployment/k8s-web-hello k8s-web-hello=arjunsreekumar/k8s-web-hello:3.0.0
kubectl rollout restart deployment k8s-web-hello
```

### Rollback

```bash
kubectl rollout undo deployment k8s-web-hello
```

---

## ðŸ“¦ Another Example: `k8s-web-to-nginx`

```bash
docker push arjunsreekumar/k8s-web-to-nginx:v11

kubectl set image deployment/k8s-web-to-nginx   k8s-web-to-nginx=arjunsreekumar/k8s-web-to-nginx:v11

kubectl rollout status deployment/k8s-web-to-nginx
kubectl rollout restart deployment/k8s-web-to-nginx

minikube service k8s-web-to-nginx
```

---

## ðŸ§¹ Clean Up

Delete all Kubernetes resources:

```bash
kubectl delete all --all
```

> Note: Kubernetes services will be recreated after deletion if defined in configuration.

---

## ðŸ“˜ Notes

- `Mi` = Mebibytes (used for memory limits)
- `500m` CPU = 0.5 vCPU (milliCPU)
- Rolling updates mean new pods are created and old ones are terminated gradually.
- Pods automatically replace themselves if deleted in a deployment context.

---

## ðŸ“¬ Questions or Feedback?

Feel free to open an issue or pull request on this repository to suggest improvements or ask questions.