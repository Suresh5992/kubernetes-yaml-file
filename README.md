# kubernetes-yaml-file
Kubernetes  yaml files from the scratch with proper explanation easy to understand 

 # Django-Three-Tier-Manifests/ directory structure in a table format including ConfigMaps, Ingress, and PVCs:

 | Directory   | File Name         | Description                     |
| ----------- | ----------------- | ------------------------------- |
| `backend/`  | `deployment.yaml` | Backend Deployment              |
|             | `service.yaml`    | Backend Service                 |
|             | `configmap.yaml`  | Backend ConfigMap               |
|             | `pvc.yaml`        | Backend Persistent Volume Claim |
| `db/`       | `deployment.yaml` | Database Deployment             |
|             | `service.yaml`    | Database Service                |
|             | `configmap.yaml`  | DB ConfigMap                    |
|             | `pvc.yaml`        | DB Persistent Volume Claim      |
| `frontend/` | `deployment.yaml` | Frontend Deployment             |
|             | `service.yaml`    | Frontend Service                |
|             | `configmap.yaml`  | Frontend ConfigMap              |
| *(root)*    | `namespace.yaml`  | Namespace Definition            |
|             | `ingress.yaml`    | Ingress Resource                |


 # Deployments, StatefulSets, DaemonSets, etc.

| Controller Type  | Purpose                                                                                             | Typical Use Case                                                          |
| ---------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Deployment**   | Manages stateless applications. Supports scaling, rolling updates, etc.                             | Web apps, APIs, frontends, backend services                               |
| **StatefulSet**  | Manages stateful applications. Maintains identity and storage per pod.                              | Databases (e.g., PostgreSQL, MongoDB), Kafka                              |
| **DaemonSet**    | Ensures a pod runs on **every** (or selected) node.                                                 | Node monitoring, log collection (e.g., Prometheus Node Exporter, Fluentd) |
| **Job**          | Runs a pod to completion (batch processing).                                                        | One-time tasks like backups, batch jobs                                   |
| **CronJob**      | Runs Jobs on a scheduled basis.                                                                     | Scheduled tasks like nightly DB dumps                                     |
| **ReplicaSet**\* | Ensures a specified number of pod replicas are running. *(Usually managed by Deployments directly)* | Internal use by Deployment                                                |


# apiVersion  for kinds
1. apiVersion – API group and version used.
2. kind – Type of Kubernetes object.
 
 
 | Kind        | apiVersion             |
| ----------- | ---------------------- |
| Deployment  | `apps/v1`              |
| Service     | `v1`                   |
| ConfigMap   | `v1`                   |
| Secret      | `v1`                   |
| Ingress     | `networking.k8s.io/v1` |
| StatefulSet | `apps/v1`              |
| Pod         | `v1`                   |



# This is Manifest 

| Resource Type         | `kind` in Manifest | Purpose                             |
| --------------------- | ------------------ | ----------------------------------- |
| Pod                   | `Pod`              | Smallest deployable unit            |
| Deployment            | `Deployment`       | Manage stateless apps               |
| Service               | `Service`          | Expose apps to the network          |
| ConfigMap             | `ConfigMap`        | Store non-confidential config       |
| Secret                | `Secret`           | Store sensitive data like passwords |
| Ingress               | `Ingress`          | HTTP(S) routing rules               |
| PersistentVolumeClaim | `PVC`              | Request storage resources           |



# 📌 Key Sections in a Manifest:
# apiVersion – API group and version used.

# kind – Type of Kubernetes object.

# metadata – Name, labels, annotations, etc.

# spec – Specifications that define the object’s desired state.


✅ Quick Summary:
🟢 Horizontal Pod Autoscaler (HPA)
👉 "Pod Replica Scaling"

Controls how many pods should run.

Increases or decreases pod replicas based on CPU, memory, or custom metrics.

🚀 Example:
If CPU usage is high → Add more pods.
If CPU usage is low → Remove some pods.

🟡 Vertical Pod Autoscaler (VPA)
👉 "Pod Size Scaling"

Controls how much CPU or Memory each pod should have.

Increases or decreases resources inside the pod.

Usually restarts the pod to apply changes.

🚀 Example:
If a pod needs more memory → VPA increases the pod’s memory.
If a pod is using very little → VPA can reduce the allocated CPU/memory.

🔥 Super Simple:
| Feature         | HPA                | VPA                     |
| --------------- | ------------------ | ----------------------- |
| Scales          | Number of Pods     | CPU/Memory per Pod      |
| Example         | 3 Pods → 5 Pods    | 500Mi → 800Mi Memory    |
| Action          | More/less replicas | Bigger/smaller pod size |
| Restart Needed? | No                 | Yes (usually)           |



✅ Example:
If traffic increases:
👉 HPA adds pods to handle more requests.

If a pod needs more memory:
👉 VPA increases the pod’s memory to avoid crashes.

#which is best HPA or  VPA

✅ HPA vs VPA: Which is Best?

| Feature                    | Horizontal Pod Autoscaler (HPA)                       | Vertical Pod Autoscaler (VPA)            |
| -------------------------- | ----------------------------------------------------- | ---------------------------------------- |
| **Scaling Type**           | Number of Pods (replicas)                             | CPU/Memory per Pod                       |
| **Best For**               | Traffic spikes, load balancing                        | Unpredictable memory/CPU usage per pod   |
| **Pod Restart Needed?**    | No                                                    | Yes (to apply changes)                   |
| **Response Time**          | Fast (spins up new pods quickly)                      | Slow (needs pod restart to resize)       |
| **Typical Use Case**       | Web servers, stateless apps, APIs                     | Databases, memory-heavy apps, batch jobs |
| **Limits**                 | May hit resource limits if pods are under-provisioned | Cannot handle sudden traffic spikes      |
| **Custom Metrics Support** | Yes                                                   | No (works based on CPU/memory only)      |


✅ When to Use HPA
Applications where traffic load changes quickly.

You need to scale out/in fast without restarting pods.

Example: Web servers, APIs, microservices.

✅ When to Use VPA
Applications where CPU/Memory usage changes unpredictably.

Pod resource requests are hard to estimate.

Example: Databases, machine learning workloads, batch processing.

✅ When to Use Both HPA + VPA
Modern Kubernetes setups often combine both for best results:

👉 HPA handles traffic load (replica scaling).

👉 VPA optimizes pod resource requests (so that each pod is correctly sized).

⚙️ But:
When combining, you should:

Use HPA based on custom metrics (like QPS) instead of just CPU, to avoid conflicts.

Use VPA in 'Initial' mode (so it sets resources when pods start, but doesn’t trigger restarts).

| Scenario                                  | Best Choice |
| ----------------------------------------- | ----------- |
| Fast traffic changes (Web app)            | HPA         |
| Heavy CPU/memory load (DB, ML)            | VPA         |
| Dynamic web app with resource fluctuation | HPA + VPA   |



