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
