# Kubernetes Learning: Core Components Deep Dive

## 📌 Overview
Building on the foundations of K8s, this session explores the specific components used to deploy a full-stack application. We use a practical example of a **JavaScript Application** connected to a **MongoDB Database** to understand the role of each object.

---

## 📦 1. The Pod: The Smallest Unit
* **Abstraction Layer:** A Pod is a wrapper around a container. Kubernetes interacts with the Pod level to remain "Container Runtime Agnostic" (you can swap Docker for other technologies easily).
* **Ephemeral Nature:** Pods are designed to be temporary. If a Pod crashes, it is replaced by a new one with a **new IP address**.



---

## 🌐 2. Networking: Services & Ingress

### Services (Permanent IP)
Since Pod IPs are unstable, a **Service** provides a static, permanent IP address.
* **Internal Service:** Used for communication between pods (e.g., App talking to MongoDB).
* **External Service:** Used to expose the app to the outside world (via NodeIP:Port).

### Ingress (Domain Routing)
Instead of accessing an app via an IP and Port, **Ingress** acts as the entry point that routes traffic using human-readable domain names (e.g., `https://my-app.com`).



---

## ⚙️ 3. Configuration & Security

### ConfigMap
Used for **External Configuration**. Instead of hardcoding a database URL inside your application image, you store it in a ConfigMap. This allows you to change settings without rebuilding your Docker image.

### Secrets
Similar to ConfigMaps but specifically for **Sensitive Data** (passwords, API keys, certificates). 
* Data is stored in **Base64 encoding**. 
* *Note:* Base64 is not encryption; it is just a way to hide plain text from casual view.

---

## 💾 4. Data Persistence: Volumes
In K8s, if a Pod dies, the data inside it is lost. To solve this, we use **Volumes**.
* **Storage Attachment:** A Volume plugs an external hard drive (local or cloud-based) into the Pod.
* **Persistence:** If the Pod restarts, the new Pod "plugs back into" the same storage, ensuring no data loss.

---

## 🚀 5. Scaling: Deployments vs. StatefulSets

### Deployments (Stateless Apps)
A **Deployment** is a blueprint for Pods. It defines how many replicas (clones) of an application should run.
* Best for **Stateless** apps (Web servers, APIs).
* If one replica dies, the Deployment ensures another one starts immediately.

### StatefulSets (Stateful Apps)
Used for **Databases** (MySQL, MongoDB, Postgres).
* It manages replicas but ensures that data writes/reads are synchronized across all clones to prevent data corruption.
* **Pro-tip:** Because StatefulSets are complex, many teams host databases *outside* the K8s cluster and only keep the application inside.



---

## 🎯 Summary Checklist

| Component | Purpose |
| :--- | :--- |
| **Pod** | Runs the container. |
| **Service** | Stable IP & Load Balancing. |
| **Ingress** | External Domain routing. |
| **ConfigMap** | Non-sensitive settings. |
| **Secret** | Credentials & Passwords. |
| **Volume** | Long-term data storage. |
| **Deployment** | Scaling stateless apps. |
| **StatefulSet** | Scaling databases. |

---
