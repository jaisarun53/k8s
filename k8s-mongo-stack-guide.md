# Complete Application Deployment: MongoDB & Mongo Express


This tutorial demonstrates a full-stack deployment of a database (MongoDB) and its web interface (Mongo Express) using a coordinated setup of Kubernetes components.

---

### 1. The Deployment Architecture
The application is structured into two main tiers to demonstrate internal vs. external communication:

* **Backend (MongoDB):** A pod running the database, hidden from the public and exposed only via an **Internal Service (ClusterIP)**.
* **Frontend (Mongo Express):** A web-based UI that connects to the backend and is accessible to users via an **External Service (LoadBalancer)**.



---

### 2. Configuration Components
Managing a real application requires more than just Pods and Services:

* **Secrets:** Used to store sensitive data like the database root password. Values must be **Base64 encoded** (e.g., `echo -n 'password' | base64`).
* **ConfigMaps:** Used for non-sensitive configuration, such as the database URL. In K8s, the URL for a database is simply the **Service Name** of the database component.
* **Environment Variables:** The Deployment files reference both Secrets and ConfigMaps to pass these values into the application containers at runtime.

---

### 3. Step-by-Step Implementation Flow
To ensure successful deployment, components should be created in a specific order:

1.  **Secret:** Define credentials first so the database deployment can find them.
2.  **MongoDB Deployment & Service:** Launch the database and create a `ClusterIP` service so it has a stable internal address.
3.  **ConfigMap:** Store the MongoDB service name so the frontend knows where to look.
4.  **Mongo Express Deployment:** Launch the web UI, referencing the Secret and ConfigMap for its connection settings.
5.  **External Service:** Create a service of `type: LoadBalancer` with a `nodePort` (range 30000-32767) to open the application to a browser.



---

### 4. Essential Kubectl Commands
These commands were used to orchestrate and verify the deployment:

| Task | Command |
| :--- | :--- |
| **Encode Secret** | `echo -n 'admin' | base64` |
| **Apply Config** | `kubectl apply -f [file].yaml` |
| **Check Logs** | `kubectl logs [pod-name]` (Verify DB connection) |
| **View All** | `kubectl get all` |
| **Minikube Access**| `minikube service [service-name]` (Opens external URL) |

---
**Key Takeaway:** In a real-world scenario, you should never hardcode credentials. Always use **Secrets** and **ConfigMaps** to keep your Deployment blueprints clean and secure.
