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
