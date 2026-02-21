# Technical Documentation: Kubernetes Namespaces
*Based on the Tutorial by TechWorld with Nana*

## 1. Overview
A **Namespace** is a logical partition or a "virtual cluster" within a physical Kubernetes cluster. It is the primary way to organize resources, manage security, and handle multi-tenancy.



---

## 2. Built-in Namespaces
When you initialize a cluster, Kubernetes provides four default namespaces:

| Namespace | Usage & Description |
| :--- | :--- |
| **`default`** | The default landing zone for any resource created without a specific namespace tag. |
| **`kube-system`** | Contains system processes, master managing processes (API server, controller), and `kubectl` components. **Avoid modifying this.** |
| **`kube-public`** | Contains publicly accessible data, including a ConfigMap with cluster information that is readable without authentication. |
| **`kube-node-lease`** | A recent addition that holds node heartbeat objects to determine node availability. |

---

## 3. Core Use Cases
Namespaces are used to solve several organizational and technical challenges:

### A. Logical Grouping
Prevents the `default` namespace from becoming cluttered. Resources can be grouped by function, such as:
* `database`
* `monitoring` (Prometheus, Grafana)
* `elastic-stack`
* `nginx-ingress`

### B. Team Isolation & Conflict Avoidance
Multiple teams can use the same cluster without interference.
* **Conflict Prevention:** Two different teams can deploy an app named `api-service` as long as they are in different namespaces.
* **Access Control (RBAC):** You can grant a team access to "Update" or "Delete" resources *only* within their specific namespace.

### C. Environment Management
Host different stages of the application lifecycle (Development, Staging, Production) in a single cluster. This allows them to share common resources like Ingress Controllers or Logging systems while remaining isolated.

### D. Resource Quotas
Administrators can limit the amount of **CPU, RAM, and Storage** a specific namespace can consume. This prevents one team's "heavy" application from starving other teams of cluster resources.

---

## 4. Key Characteristics
* **Isolation of Resources:** ConfigMaps and Secrets are restricted to their own namespace. A Pod in `Project-A` cannot use a Secret from `Project-B`.
* **Cross-Namespace Services:** Services can be shared. A Pod can access a database in another namespace via the URL: `[service-name].[namespace-name]`.
* **Global Resources:** Not all resources are namespaced. Components like **Nodes**, **Persistent Volumes**, and **StorageClasses** exist globally across the cluster.

---

## 5. Implementation Guide

### CLI Commands
```bash
# Create a namespace via CLI
kubectl create namespace production

# List all namespaces
kubectl get namespaces

# List resources that ARE NOT namespaced (Global)
kubectl api-resources --namespaced=false

# List resources that ARE namespaced
kubectl api-resources --namespaced=true
```
### Best Practice: Declarative YAML

It is best practice to define the namespace in the metadata of your configuration files for better documentation and automation.
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: development  # Explicitly defined here
data:
  db_url: "postgres://db-service"
  ```
### Productivity Tools

To avoid typing -n <namespace> repeatedly, use kubens (part of the kubectx suite):
```
# Switch active namespace context
kubens development
```
  
