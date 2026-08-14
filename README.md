 # CNE Independent Project 3 - Kubernetes Workloads

## Project Overview
This project is a continuation of [CNE01 Independent Project 2 - Containerization](https://github.com/KarenNgugi/CNE01-Independent_Project_2) which sets up a 3-tier web application that allows students to be added, grades to be recorded, and results to be viewed. In this project, the workflow will be updated to include Kubernetes and its components.

Upon completion of this project, the following will be demonstrated:
* How to write Kubernetes manifests for real application workloads
* How to deploy a three-tier application using Deployments and a StatefulSet
* How to expose application tiers using appropriate Service types
* How to manage application configuration using ConfigMaps
* How to persist database data using PersistentVolumes and PersistentVolumeClaims
* How to apply resource requests and limits to all workloads
* How to organise manifests clearly and apply them in the correct order
* How to troubleshoot Kubernetes workload issues using kubectl
* How to document Kubernetes architecture professionally on GitHub

## Prerequisites
You need the following to be able to run the application:
- git
- Docker
- Minikube
- kubectl

## Quick Start
```
# create project folder and navigate into it
mkdir kubernetes_project; cd $_

# clone the project
git clone git@github.com:KarenNgugi/CNE01-Independent_Project_3.git .

# start Minikube
minikube start --driver=docker

# move into the Kubernetes scripts folder
cd kubernetes/scripts

# run the script to apply all manifests
./apply

# obtain app URL 
minikube service frontend-svc --url
```

Access the application in the browser using the provided URL. When done, run the following to delete the resources (remember to be in `kubernetes/scripts/`):
```
./delete
```

More information about the Kubernetes manifests, including **step-by-step instructions** can be found at [the Kubernetes README.md](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/feat/kubernetes/kubernetes/README.md).


## Architecture*

## Resources*

| Resource | Name | Description | Defined By |
| ----- | ----- | ----- | ----- |
| Namespace | `grades-tracker-namespace` | The environment that will contain the specific Grades Tracker resources | namespace.yaml |
| Secret | `postgres-password` | The database password | `kubectl create secret` |
| Secret | `db-password` | The password used by the backend to connect to the database | `kubectl create secret` |
| ConfigMap | `init-db` | Initializes the database | `kubectl create configmap` |
| ConfigMap | `database-configmap` | Provides non-sensitive environment variables that will be consumed by the database | configmap.yaml |
| ConfigMap | `backend-configmap` | Provides non-sensitive environment variables that will be consumed by the backend | configmap.yaml |
| PersistentVolume | `grades-tracker-pv` | The volume that will permanently store the data from the Grades Tracker application | persistent-volume.yaml |
| PersistentVolumeClaim | `grades-tracker-pvc` | Makes a request for a volume with specific resources | persistent-volume-claim.yaml |
| Service | `database-svc` | Provides a stable internal endpoint through which the backend accesses PostgreSQL | postgres-service.yaml |
| Service | `headless-svc` | Provides a DNS-based network identity/discovery for the database's Pods | postgres-headless-service.yaml |
| StatefulSet | `grades-tracker-statefulset` | Sets up the database | postgres-statefulset.yaml |
| Service | `tracker-backend` | Provides a stable internal endpoint through which the frontend accesses the backend | backend-service.yaml |
| Deployment | `grades-tracker-backend-deployment` | Sets up the backend | backend-deployment.yaml |
| Service | `frontend-svc` | Provides a stable internal endpoint through which the backend accesses the frontend | frontend-service.yaml |
| Deployment | `grades-tracker-frontend-deployment` | Sets up the frontend | frontend-deployment.yaml |

## Troubleshooting Guide


## Author Information
Author: [Karen Ngugi](https://github.com/KarenNgugi)
