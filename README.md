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

# run the script to apply all manifests
./kubernetes/scripts/apply

# obtain app URL 
minikube service frontend-svc --url
```

Access the application in the browser. When done, run the following to delete the resources:
```
./kubernetes/scripts/delete
```

More information about the Kubernetes manifests can be found [here](https://github.com/KarenNgugi/CNE01-Independent_Project_3/blob/feat/kubernetes/kubernetes/README.md).


## Architecture*

## Resources*

| Resource | Name | Description | Created Through |
| ----- | ----- | ----- | ----- |
| Namespace | `grades-tracker-namespace` |  | namespace.yaml |
| Secret | `db-password` |  | `kubectl create secret` |
| Secret | `postgres-password` |  | `kubectl create secret` |
| ConfigMap | `init-db` |  | `kubectl create configmap` |
| ConfigMap | `database-configmap` |  | configmap.yaml |
| ConfigMap | `backend-configmap` |  | configmap.yaml |
| PersistentVolume | `grades-tracker-pv` |  | persistent-volume.yaml |
| PersistentVolumeClaim | `grades-tracker-pvc` |  | persistent-volume-claim.yaml |
| Service | `database-svc` |  | postgres-service.yaml |
| Service | `headless-svc` |  | postgres-headless-service.yaml |
| StatefulSet | `grades-tracker-statefulset` |  | postgres-statefulset.yaml |
| Service | `tracker-backend` |  | backend-service.yaml |
| Deployment | `grades-tracker-backend-deployment` |  | backend-deployment.yaml |
| Service | `frontend-svc` |  | frontend-service.yaml |
| Deployment | `grades-tracker-frontend-deployment` |  | frontend-deployment.yaml |

## Troubleshooting Guide


## Author Information
Author: [Karen Ngugi](https://github.com/KarenNgugi)
