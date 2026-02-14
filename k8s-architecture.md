# Kubernetes Learning: Architecture Deep Dive

## 📌 Overview
This session explains the internal mechanisms of Kubernetes. While K8s is a powerful framework, its complexity comes from the various processes that work together to automate container orchestration. We look at the specific roles of **Master Nodes** and **Worker Nodes**.

---

## 👷 1. Worker Node Architecture
Worker nodes are the servers that do the actual work of running your application pods. Every worker node must have three specific processes installed:

* **Container Runtime:** (e.g., Docker, containerd). A runtime is necessary to execute the containers inside the pods.
* **Kubelet:** The primary "node agent." It interacts with both the container runtime and the node's resources (CPU, RAM). It is responsible for taking instructions from the Master and starting/stopping containers.
* **Kube-Proxy:** An intelligent network proxy. It handles network communication between services and pods, ensuring requests are routed efficiently (e.g., preferring pods on the same node to reduce latency).



---

## 🧠 2. Master Node Architecture (Control Plane)
Master nodes manage the cluster state and oversee the worker nodes. They run four critical processes:

* **API Server:** The cluster's "Gateway." It is the only entry point for users (via `kubectl` or UI) and acts as the gatekeeper for authentication and authorization.
* **Scheduler:** The "Decision Maker." When you request a new pod, the API server hands it to the scheduler. It analyzes worker node resources (CPU/RAM) and chooses the best node for the job.
* **Controller Manager:** The "Repairman." It monitors the cluster for state changes (like a pod crashing). If a pod dies, it detects the failure and requests a reschedule.
* **etcd:** The "Cluster Brain." A distributed key-value store that keeps the current state of the cluster. It acts as the "Source of Truth."



---

## 🔄 3. How they Work Together (The Lifecycle)
1.  **Request:** A user sends a deployment command to the **API Server**.
2.  **Schedule:** The **API Server** validates the request and hands it to the **Scheduler**.
3.  **Deploy:** The **Scheduler** identifies the best node and tells the **Kubelet** on that node to start the pod.
4.  **Monitor:** If a pod crashes, the **Controller Manager** detects the discrepancy and triggers the restart cycle.
5.  **Record:** Every single status change is logged in **etcd** to ensure the cluster is synchronized.

---

## 🏢 4. Realistic Cluster Setup
In production environments, clusters are distributed for High Availability (HA):
* **Multiple Masters:** Usually 2-3 master nodes are used so that if one fails, the cluster remains operational.
* **Resource Allocation:** Master nodes require fewer resources (CPU/RAM) because they don't run heavy application code. Worker nodes require more power to handle the actual user traffic and application workloads.



---

## 🎯 Summary Checklist

| Component | Node Type | Role |
| :--- | :--- | :--- |
| **API Server** | Master | Cluster Gateway & Authentication |
| **Scheduler** | Master | Resource-based Scheduling |
| **Controller Manager** | Master | State monitoring & Self-healing |
| **etcd** | Master | Cluster State Storage (Key-Value) |
| **Kubelet** | Worker | Starting/Stopping Containers |
| **Kube-Proxy** | Worker | Network Routing |

---
