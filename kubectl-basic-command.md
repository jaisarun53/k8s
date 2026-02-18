# Kubernetes Learning: Kubectl Basic Commands & Debugging

## 📌 Overview
This session covers the fundamental interaction with a Kubernetes cluster using `kubectl`. We move from imperative commands (command line) to declarative configuration (YAML files), while mastering the tools needed to troubleshoot failing pods.

---

## 🏗️ 1. The Kubernetes Hierarchy
In practice, we don't manage Pods directly. We manage **Deployments**.



* **Deployment**: The blueprint (defines image, replicas, etc.).
* **ReplicaSet**: The manager (ensures the correct number of pods are running).
* **Pod**: The smallest unit (an abstraction of a container).

---

## 🛠️ 2. Essential CRUD Operations
Common commands to Create, Read, Update, and Delete resources.

| Action | Command | Description |
| :--- | :--- | :--- |
| **Create** | `kubectl create deployment [name] --image=[img]` | Creates a new deployment & pod. |
| **Get** | `kubectl get pod / deployment / replicaset` | Lists the status of resources. |
| **Edit** | `kubectl edit deployment [name]` | Opens the live configuration in a text editor. |
| **Delete** | `kubectl delete deployment [name]` | Removes the deployment and all its pods. |

---

## 🔍 3. The Debugging Toolkit
When a pod status shows `ContainerCreating`, `Error`, or `CrashLoopBackOff`, use these three steps in order:

### Step 1: `kubectl logs [pod_name]`
Shows the application's internal output. Useful if the app crashed due to a code error or database connection failure.

### Step 2: `kubectl describe pod [pod_name]`
Shows a timeline of events. Use this if the pod won't even start (e.g., `ImagePullBackOff` or `Insufficient CPU`).



### Step 3: `kubectl exec -it [pod_name] -- bin/bash`
Drops you into a terminal inside the container. Use this to check files, environment variables, or network connectivity from within the pod.

---

## 📄 4. The Declarative Way: `kubectl apply`
Instead of long CLI commands, we use **YAML configuration files**. This allows for version control and easier management of complex setups.

**The Workflow:**
1.  Create/Update a file (e.g., `nginx.yaml`).
2.  Run: `kubectl apply -f nginx.yaml`.

> **Note:** `apply` is smart. If the resource doesn't exist, it creates it. If it does exist, it only updates the differences.

---

## 🎓 Summary Checklist
- [x] Use **Deployments** to manage Pods.
- [x] Check **ReplicaSet** if pods aren't scaling correctly.
- [x] Use **Describe** for K8s infrastructure issues and **Logs** for application issues.
- [x] Always prefer `apply -f` for production environments.
### B. Declarative (YAML) - *Best Practice*
Create a file named `nginx-deployment.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
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
        image: nginx:1.16
        ports:
        - containerPort: 80

