# kubernetes-yaml-file
Kubernetes  yaml files from the scratch with proper explanation easy to understand 
**Edit and see it **
Django-Three-Tier-Manifests/
├── backend/
│   ├── deployment.yaml
│   └── service.yaml
├── db/
│   ├── deployment.yaml
│   └── service.yaml
├── frontend/
│   ├── deployment.yaml
│   └── service.yaml
└── namespace.yaml

 Deployments, StatefulSets, DaemonSets, etc.
 
 | Kind        | apiVersion             |
| ----------- | ---------------------- |
| Deployment  | `apps/v1`              |
| Service     | `v1`                   |
| ConfigMap   | `v1`                   |
| Secret      | `v1`                   |
| Ingress     | `networking.k8s.io/v1` |
| StatefulSet | `apps/v1`              |
| Pod         | `v1`                   |





| Resource Type         | `kind` in Manifest | Purpose                             |
| --------------------- | ------------------ | ----------------------------------- |
| Pod                   | `Pod`              | Smallest deployable unit            |
| Deployment            | `Deployment`       | Manage stateless apps               |
| Service               | `Service`          | Expose apps to the network          |
| ConfigMap             | `ConfigMap`        | Store non-confidential config       |
| Secret                | `Secret`           | Store sensitive data like passwords |
| Ingress               | `Ingress`          | HTTP(S) routing rules               |
| PersistentVolumeClaim | `PVC`              | Request storage resources           |

