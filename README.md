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
