# Minikube & Kubectl

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
Initialize a Kubernetes cluster locally using Minikube. This will start a virtual machine or container running Kubernetes.
```sh
minikube start
```
Minikube automatically configures `kubectl` to interact with this cluster.

### Step 2: Verify Cluster Status
After Minikube starts, verify that your Kubernetes cluster is running properly:
```sh
kubectl get nodes
```
You should see a node with a **Ready** status, indicating that your local cluster is up and running.

### Step 3: Create a Deployment
Deploy an **nginx** web server in Kubernetes to demonstrate how deployments work:
```sh
kubectl create deployment nginx --image=nginx
```
This command creates a deployment named `nginx` using the official `nginx` container image from Docker Hub.

### Step 4: Expose the Deployment
Expose the deployment using a **NodePort** service to make it accessible outside the cluster:
```sh
kubectl expose deployment nginx --type=NodePort --port=80
```
This will assign a port from the range 30000-32767, which will allow you to access the service externally.

### Step 5: Retrieve the Service URL
To access the exposed service, retrieve its URL using Minikube:
```sh
minikube service nginx --url
```
This outputs a URL like `http://192.168.99.100:30001`, which you can open in a browser to see the **nginx** welcome page.

### Step 6: Check Running Pods
View all running pods in the cluster:
```sh
kubectl get pods
```
Each pod runs an instance of the container specified in the deployment. The `STATUS` should be `Running` if everything is working correctly.

### Step 7: Scale the Deployment
Increase the number of running instances (replicas) to handle more traffic:
```sh
kubectl scale deployment nginx --replicas=3
```
Verify that new pods are created:
```sh
kubectl get pods
```
You should now see three running nginx pods.

### Step 8: Clean Up
When finished, delete the deployment and service to free resources:
```sh
kubectl delete service nginx
kubectl delete deployment nginx
```
This removes all associated pods and resources from the cluster.

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



