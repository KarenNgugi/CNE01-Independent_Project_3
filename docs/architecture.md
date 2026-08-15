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

## 2. Deployment/StatefulSet Level

### 2.1. Frontend Deployment
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/frontend-deployment-architecture.png)

### 2.2. Backend Deployment
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/backend-deployment-architecture.png)

### 2.3. Database StatefulSet
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/database-statefulset-architecture.png)

## 3. Pod Level
### 3.1. Frontend Pod
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/frontend-pod-architecture.png)

### 3.2. Backend Pod
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/backend%20pod%20architecture.png)

### 3.3. Database Pod
![](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/docs/architecture/docs/database%20pod%20architecture.png)

---

# Resources

---

# Design Decisions

---

# ReplicaSet Exercise Observations

---

# Challenges Faced
