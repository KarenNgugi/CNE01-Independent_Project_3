 # CNE Independent Project 3 - Kubernetes Workloads

## Project Overview
This project is a continuation of [CNE01 Independent Project 2 - Containerization](https://github.com/KarenNgugi/CNE01-Independent_Project_2) which sets up a 3-tier web application that allows students to be added, grades to be recorded, and results to be viewed. In this project, the workflow will be updated to include Kubernetes and its components.


Upon completion of this project, I will be able to demonstrate how to:
* Write Kubernetes manifests for real application workloads
* Deploy a three-tier application using Deployments and a StatefulSet
* Expose application tiers using appropriate Service types
* Manage application configuration using ConfigMaps
* Persist database data using PersistentVolumes and PersistentVolumeClaims
* Apply resource requests and limits to all workloads
* Organise manifests clearly and apply them in the correct order
* Troubleshoot Kubernetes workload issues using kubectl
* Document Kubernetes architecture professionally on GitHub

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

## Troubleshooting Guide


## Author Information
Author: [Karen Ngugi](https://github.com/KarenNgugi)
