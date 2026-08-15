# Student Grade Tracker Architecture

## Overview

In the [Containerization Project](https://github.com/KarenNgugi/CNE01-Independent_Project_2/), we established the architecture of the application and the container setup:
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/ip2%20architecture.png)

Further details of such can be found [here](https://github.com/KarenNgugi/CNE01-Independent_Project_2/blob/main/docs/architecture.md).

In this document, we will look at the Kubernetes architecture which covers the following:
* Pods
* Services
* Deployments & StatefulSets
* PersistentVolumes
* PersistentVolumeClaims
* ConfigMaps & Secrets

---

# Diagrams
## 1. High Level Overview
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/High%20Level%20Architecture%20Overview.png)

## 2. Tier Level

### 2.1. Frontend Tier
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/frontend-deployment-architecture.png)
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/frontend-pod-architecture.png)

### 2.2. Backend Tier
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/backend-deployment-architecture.png)
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/backend%20pod%20architecture.png)

### 2.3. Database Tier
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/database-statefulset-architecture.png)
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/database%20pod%20architecture.png)



---

# Resources

---

# Design Decisions

- Only the frontend is externally accessible. The backend and database are not exposed outside the Kubernetes cluster. This limits the attack surface and ensures that requests to the database are handled through the backend rather than directly from the frontend.
- The frontend and database do not communicate directly. All data requests between the frontend and database are routed through the backend. This provides an additional security boundary and prevents users or a potentially compromised frontend from directly accessing the database.
- Deployments are used for the frontend and backend. Both applications are stateless, making them suitable for Deployments. A Deployment manages the underlying Pods and supports controlled updates and rollbacks, avoiding the need to manually manage individual Pods as application versions change.
- A StatefulSet is used for the database. Unlike the frontend and backend, the database is stateful and requires persistent storage and a stable identity. A StatefulSet provides stable Pod identities and predictable naming, which is appropriate for workloads where the identity and persistent storage associated with a Pod need to be maintained.
- Persistent storage is used for the database. A PersistentVolume (PV) is used to store database data independently of the database container's lifecycle. This allows the data to survive events such as a database Pod being deleted or recreated.
- The backend Service is named `tracker-backend` to match the existing frontend configuration. The frontend image is configured to communicate with a backend using the hostname `tracker-backend`. Rather than rebuilding the frontend image solely to change this hostname, a Service with the expected name was created. This allows Kubernetes service discovery to resolve the hostname without modifying the frontend image.
- The PersistentVolume and PersistentVolumeClaim use an empty string for the `storageClassName`. Minikube provides a default `StorageClass` named `standard`. The `storageClassName` is intentionally set to an empty string for both the PV and PVC so that they are treated as manually managed, rather than being associated with a dynamically provisioned `StorageClass`. This allows the PV and PVC to bind based on their other matching requirements.
- Secrets are used for sensitive configuration. Sensitive values such as database passwords are stored in Kubernetes Secrets rather than being hardcoded in ConfigMaps. This separates sensitive credentials from general application configuration and reduces the risk of accidentally exposing them.
- The database StatefulSet uses the `OnDelete` update strategy. StatefulSets support `RollingUpdate` and `OnDelete` update strategies. `OnDelete` was selected because the project uses a single database Pod and database availability and data integrity are more important than automatically replacing the Pod when its specification changes. With this strategy, changes to the StatefulSet are applied to the Pod only after the existing Pod is manually deleted, allowing the database restart to be performed deliberately.
- The PersistentVolume uses a Minikube `hostPath` set to `/var/grades-tracker/postgres` for storing PostgreSQL data. Because the project is deployed and tested using Minikube, this path refers to the filesystem of the Minikube node rather than the host machine running Minikube. Consequently, the directory and its contents are managed within the Minikube environment.

---

# ReplicaSet Exercise Observations

---

# Challenges Faced

---

# Next Steps
- Create a initContainer for the backend Deployment that waits for the database to be ready before the API starts
- Incorporate Helm for packaging and easier installation
- Add healthchecks and restart policies to the Pods/containers
- Add a CONTRIBUTING.md 
