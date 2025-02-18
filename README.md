# Minikube and kubectl Lab Setup

This guide will walk you through setting up and working with **Minikube** and **kubectl** to create a local Kubernetes cluster on your laptop. By following these steps, you'll be able to deploy, manage, and scale applications using Kubernetes.

---
## Prerequisites

### Install Minikube
Minikube runs a local Kubernetes cluster inside a virtual machine (VM) or container.

- **Linux:**  
  ```sh
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
  ```
- **macOS:**  
  ```sh
  brew install minikube
  ```
- **Windows:**  
  ```sh
  choco install minikube
  ```

### Install kubectl
kubectl is the command-line tool used to interact with Kubernetes.

- **Linux/macOS:**  
  ```sh
  curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/$(uname | tr '[:upper:]' '[:lower:]')/amd64/kubectl"
  chmod +x kubectl
  sudo mv kubectl /usr/local/bin/
  ```
- **Windows:**  
  Download and install kubectl from the [official Kubernetes site](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/).

Verify installation:
```sh
kubectl version --client
```

---
## Step-by-Step Guide

### Step 1: Start Minikube
Initialize a Kubernetes cluster locally:
```sh
minikube start
```

### Step 2: Verify Cluster Status
Check if the Minikube cluster is running:
```sh
kubectl get nodes
```
You should see a node with a **Ready** status.

### Step 3: Create a Deployment
Deploy an **nginx** web server in Kubernetes:
```sh
kubectl create deployment nginx --image=nginx
```
This command creates a deployment named `nginx` using the official `nginx` container image.

### Step 4: Expose the Deployment
Expose the deployment using a **NodePort** service to make it accessible:
```sh
kubectl expose deployment nginx --type=NodePort --port=80
```

### Step 5: Retrieve the Service URL
Find the URL to access the **nginx** service:
```sh
minikube service nginx --url
```
This outputs a URL like `http://192.168.99.100:30001`, which you can open in a browser.

### Step 6: Check Running Pods
View running pods in the cluster:
```sh
kubectl get pods
```

### Step 7: Scale the Deployment
Increase the number of replicas (pods) for load balancing:
```sh
kubectl scale deployment nginx --replicas=3
```
Verify scaling:
```sh
kubectl get pods
```

### Step 8: Clean Up
When finished, delete the deployment and service:
```sh
kubectl delete service nginx
kubectl delete deployment nginx
```

---
## Full Command Workflow
```sh
# Start Minikube
minikube start

# Verify Minikube and Kubernetes cluster status
kubectl get nodes

# Create an nginx deployment
kubectl create deployment nginx --image=nginx

# Expose the nginx deployment
kubectl expose deployment nginx --type=NodePort --port=80

# Get the URL for accessing the service
minikube service nginx --url

# Check the status of running pods
kubectl get pods

# Scale the deployment to 3 replicas
kubectl scale deployment nginx --replicas=3

# Clean up (delete service and deployment)
kubectl delete service nginx
kubectl delete deployment nginx
```

---
## Conclusion
By following this guide, you have successfully:
- Set up Minikube and kubectl
- Created a local Kubernetes cluster
- Deployed and exposed an nginx web server
- Scaled the deployment
- Cleaned up the environment

Minikube is an excellent tool for testing and experimenting with Kubernetes before deploying to a production environment. 🚀


