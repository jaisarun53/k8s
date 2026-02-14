### ☸️ Kubernetes (K8s) Foundations: Orchestration Explained

This session introduces **Kubernetes**, the industry-standard container orchestration platform. We explore how it moves beyond simple container management to provide a self-healing, scalable infrastructure for microservices.

**Key Learning Objectives:**
* **What is Kubernetes?** Understanding K8s as the "Captain" of the ship, managing thousands of containers across physical or virtual machines.
* **The Master-Worker Architecture:** * **Master Node (Control Plane):** The "Brain" that handles scheduling, state management (`etcd`), and API requests.
    * **Worker Node (Data Plane):** The "Muscle" where applications actually run inside pods.
* **Core Components:**
    * **Pods:** The smallest unit in K8s (a wrapper around a container).
    * **Services:** Providing permanent IP addresses and load balancing to ephemeral pods.
* **Declarative Configuration:** Using **YAML** to define the "Desired State," allowing K8s to automatically heal and scale the cluster without manual intervention.



---
**Detailed Documentation:** [k8s-foundations.md](./k8s-foundations.md)

### 🧭 Kubernetes Components: The Building Blocks of Orchestration

This session moves from high-level architecture to the specific objects you will use daily to deploy applications. We use a practical scenario—a web app connected to a database—to define the roles of each component.

**Key Learning Objectives:**
* **The Pod vs. Container:** Why K8s uses Pods as an abstraction layer to remain independent of the underlying container runtime.
* **Networking Strategy:** * **Internal Services:** For secure, permanent communication between internal components (e.g., App to DB).
    * **Ingress:** Providing a "front door" for the cluster using domain names and SSL.
* **Configuring Environments:** * **ConfigMaps:** Decoupling application settings from the code for easier updates.
    * **Secrets:** Managing sensitive credentials and certificates safely using Base64 encoding.
* **State Management:** * **Volumes:** Attaching persistent storage to ensure data isn't lost when a pod restarts.
    * **Deployments vs. StatefulSets:** Choosing the right controller for stateless web apps versus stateful database clusters.



---
**Detailed Documentation:** [k8s-components.md](./k8s-components.md)

### 🧠 Kubernetes Architecture: Behind the Scenes

This session breaks down the complex "brain and muscle" relationship of a Kubernetes cluster. Understanding these internal processes is key to troubleshooting why a pod isn't scheduling or how self-healing works.

**Key Learning Objectives:**
* **The Master Node (Control Plane):**
    * **API Server:** The gateway for all commands and security gatekeeper.
    * **Scheduler:** The intelligent decision-maker for resource allocation.
    * **Controller Manager:** The watchman that ensures the "actual state" matches the "desired state."
    * **etcd:** The cluster's source of truth; a key-value store of every configuration and status.
* **The Worker Node (Data Plane):**
    * **Kubelet:** The agent that takes orders from the Master to run containers.
    * **Kube-Proxy:** The networking genius that routes traffic efficiently across the cluster.
    * **Container Runtime:** The engine (like Docker) that actually executes the code.
* **High Availability (HA):** Why production environments use multiple master nodes to prevent a "single point of failure."



---
**Detailed Documentation:** [k8s-architecture.md](./k8s-architecture.md)

# 🌐 Kubernetes Services: Networking Summary

In Kubernetes, Pods are dynamic and ephemeral. **Services** provide the essential networking layer that allows these pods to communicate reliably by providing a stable IP address and DNS name.

### 🔑 Key Concepts
* **Stability:** Services provide a persistent "front-end" IP that doesn't change when pods are recreated.
* **Load Balancing:** Automatically distributes traffic across all healthy pod replicas matching a selector.
* **Service Discovery:** Allows pods to find each other using standard DNS names instead of volatile IP addresses.

### 🚦 Service Types at a Glance
| Type | Visibility | Use Case |
| :--- | :--- | :--- |
| **ClusterIP** | Internal Only | Default. Inter-service communication (e.g., App to DB). |
| **Headless** | Internal Only | For StatefulSets (Databases) requiring direct Pod-to-Pod sync. |
| **NodePort** | External (Node IP) | Testing/Dev. Exposes a port (30000-32767) on every node. |
| **LoadBalancer** | External (Public IP)| Production. Native integration with Cloud provider LBs. |

### 🛠️ The "Glue": Selectors & Ports
* **Selectors:** The mechanism that links a Service to a Pod via labels.
* **Port:** The port exposed on the Service IP.
* **TargetPort:** The port the application listens on inside the container.
* **Endpoints:** The dynamic list of healthy pod IPs currently serving traffic.



---
**Full Documentation:** [Detailed Services Guide](./k8s_Services.md)

