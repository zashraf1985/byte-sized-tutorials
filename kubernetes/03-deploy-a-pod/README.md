

# How to Deploy a Pod in Kubernetes

This tutorial will walk you through deploying a simple pod in Kubernetes. A **pod** is the smallest deployable unit in Kubernetes, representing one or more containers that share the same network and storage.

## Prerequisites

Before you start, make sure you have the following tools installed:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/) - for setting up a local Kubernetes cluster
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) - Kubernetes command-line tool
- [Git](https://git-scm.com/) - to clone this repository

## Setup Instructions

### Step 1: Start Minikube

If you haven't already, start Minikube:

```bash
minikube start
```

This command will spin up a local Kubernetes cluster. It may take a few minutes, depending on your system.

### Step 2: Verify Minikube is Running

Check the status of your Minikube cluster:

```bash
minikube status
```

You should see that the components are running correctly.

### Step 3: Clone the Byte-Sized Tutorials Repository

Clone this repository to get the tutorial files:

```bash
git clone https://github.com/zashraf/byte-sized-tutorials.git
cd byte-sized-tutorials/kubernetes/03-deploy-a-pod
```

### Step 4: Deploy the Pod

To create the pod, apply the provided YAML file:

```bash
kubectl apply -f pod.yaml
```

The `pod.yaml` file contains the following configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-first-pod
spec:
  containers:
  - name: my-container
    image: nginx
    ports:
    - containerPort: 80
```

This configuration creates a pod named `my-first-pod` that runs a container using the **nginx** image, with port 80 exposed.

### Step 5: Check the Pod Status

Verify that the pod is running:

```bash
kubectl get pods
```

If the pod is running, you should see the status as `Running`.

### Step 6: Access Nginx in the Browser

1. **Expose the Pod as a Service**:
   ```bash
   kubectl expose pod my-first-pod --type=NodePort --port=80
   ```

2. **Get the Minikube IP and NodePort**:
   - Find the Minikube IP:
     ```bash
     minikube ip
     ```
   - Get the NodePort:
     ```bash
     kubectl get services
     ```

   Use the Minikube IP and NodePort to access Nginx in the browser:
   ```
   http://<Minikube-IP>:<NodePort>
   ```

### Step 7: Inspect the Pod Details

If you need more information about the pod or encounter any issues, describe the pod:

```bash
kubectl describe pod my-first-pod
```

### Step 8: Clean Up

To delete the pod and service, run:

```bash
kubectl delete pod my-first-pod
kubectl delete service my-first-pod
```

## Conclusion

Congratulations! You have successfully deployed your first pod in Kubernetes. This basic example forms the foundation for working with Kubernetes, as all higher-level components build upon pods.

Stay tuned for the next tutorial, where we’ll cover using Kubernetes deployments to manage replicas and automate updates.
