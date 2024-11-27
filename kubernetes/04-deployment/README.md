
# Understanding Kubernetes Deployments

This tutorial walks you through the basics of Kubernetes Deployments. A **deployment** is a higher-level abstraction that simplifies managing pods in Kubernetes. Deployments handle tasks like scaling, rolling updates, and rollbacks, all while ensuring your application stays available and responsive.

## Prerequisites

Before you begin, make sure you have the following tools installed and set up:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/) - for running a local Kubernetes cluster.
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) - Kubernetes command-line tool.

Ensure that Minikube is running:

```bash
minikube start
```

Verify the status of your Minikube cluster:

```bash
minikube status
```

You can find detailed setup instructions [here](https://github.com/yourusername/byte-sized-tutorials).

## Commands and Steps

### Step 1: Create a Deployment

First, create a file named `deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-first-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
```

Apply the deployment:

```bash
kubectl apply -f deployment.yaml
```

### Step 2: Verify the Deployment

Check the status of your deployment:

```bash
kubectl get deployments
```

Check the pods created by the deployment:

```bash
kubectl get pods
```

### Step 3: Update the Deployment

To update the deployment, edit the `deployment.yaml` file and update the image version:

```yaml
image: nginx:1.22
```

Reapply the updated file:

```bash
kubectl apply -f deployment.yaml
```

Check the rollout status:

```bash
kubectl rollout status deployment my-first-deployment
```

### Step 4: Rollback the Deployment

To revert to the previous configuration:

```bash
kubectl rollout undo deployment my-first-deployment
```

### Step 5: Scale the Deployment

Scale the deployment to handle more traffic:

```bash
kubectl scale deployment my-first-deployment --replicas=5
```

Verify the scaling:

```bash
kubectl get pods
```

### Cleanup

When you’re done, delete the deployment:

```bash
kubectl delete deployment my-first-deployment
```

## What’s Next?

In the next tutorial, we’ll explore **Kubernetes Services** and learn how to expose your application to the outside world.

---

This tutorial introduces manual scaling and rolling updates. For dynamic adjustments based on resource usage, check out our upcoming tutorial on **Horizontal Pod Autoscaling**.
