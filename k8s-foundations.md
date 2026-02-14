# Kubernetes (K8s) Learning: What is Kubernetes?

## 📌 Overview
This session covers the fundamentals of **Kubernetes (K8s)**, an open-source container orchestration framework originally developed by Google. Kubernetes is designed to automate the deployment, scaling, and management of containerized applications.

---

## 🏗️ 1. Why Kubernetes? (The Problem & Solution)
With the shift toward **microservices**, applications are now broken into hundreds or thousands of containers. Managing these manually is impossible. 

### Core Orchestration Benefits:
* **High Availability:** Ensures your application has no downtime; it is always accessible to users.
* **Scalability:** Automatically handles increased traffic by scaling resources up or down to maintain performance.
* **Disaster Recovery:** If a server fails, K8s detects the failure and restores the application to its latest stable state using backups from `etcd`.



[Image of monolithic vs microservices architecture]


---

## 🏛️ 2. Kubernetes Architecture
A Kubernetes cluster is built on a **Master-Worker** relationship.

### A. The Master Node (The Control Plane)
The Master node acts as the "Brain" of the cluster, running these essential processes:
* **API Server:** The front-end of the cluster; every command (CLI, UI, or Script) goes through here.
* **Scheduler:** Decides which worker node is best suited to run a new pod based on resource availability.
* **Controller Manager:** Monitors the cluster state. If a container crashes, it triggers a restart to maintain the "desired state."
* **etcd:** A high-availability key-value store that acts as the cluster's "Memory," holding all configuration and status data.



### B. The Worker Nodes (The Data Plane)
This is where the actual application workload runs:
* **Kubelet:** An agent that ensures containers are running in a pod and communicates back to the Master node.
* **Container Runtime:** The software (like Docker or containerd) responsible for running the containers.

---

## 📦 3. Core K8s Components

### Pods
* **Definition:** The smallest deployable unit in K8s. 
* **Function:** A pod is a wrapper around a container. While a pod can hold multiple containers, the standard practice is **one container per pod**.
* **IP Address:** Every pod gets a unique internal IP address for communication.
* **Ephemeral:** Pods are temporary. If a pod dies, K8s creates a new one with a *new* IP address.

### Services
* **Definition:** A static entry point for a group of pods.
* **Function:** Since pod IPs change, a **Service** provides a permanent IP address that acts as a Load Balancer, ensuring communication remains stable even if pods are recreated.



---

## 📄 4. How Configuration Works
Kubernetes is **Declarative**. You don't tell K8s "how" to do something; you tell it "what" you want the final state to look like using **YAML** files.

1.  **Desired State:** You define that you want "3 replicas of a web server."
2.  **Actual State:** K8s checks how many are currently running.
3.  **Self-Healing:** If only 2 are running, the Controller Manager sees the discrepancy and automatically starts a 3rd pod.

### Example Deployment Blueprint:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```
## 🎯 Summary
Kubernetes is the "Orchestrator" that manages the lifecycle of containers.

It simplifies scaling and fault tolerance, allowing engineers to focus on code rather than infrastructure maintenance.

It turns a collection of servers into a single, unified computing resource.
