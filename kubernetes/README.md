# Running the app in Kubernetes

## Prerequisites
- kubectl
- Minikube
- Docker

## Process
Make sure you are in the `kubernetes` directory:
```
cd kubernetes
```

Start Minikube:
```
minikube start --driver=docker
```

### 1. Namespace
Run:
```
kubectl apply namespace.yaml
```

### 2. Context, Secrets, & database initialization ConfigMap
#### 2.1. Manually
To set the newly created `grades-tracker-namespace` as the default namespace so that you don't have to keep adding `-n grades-tracker-namespace`, run:
```
kubectl config set-context --current --namespace=grades-tracker-namespace
```

To create the Secret for the backend containers to connect to the database container, run:
```
kubectl create secret generic db-password --from-literal=DB_PASSWORD="password"
```

To create the Secret for the PostgreSQL database password, run:
```
kubectl create secret generic postgres-password --from-literal=POSTGRES_PASSWORD="password"
```

To create the ConfigMap that initializes the database, run:
```
kubectl create configmap init-db --from-file=../database/init.sql
```

**Note:** it is safer to use secrets than to hardcode sensitive information.

#### 2.2. Using the `context` script file
Run:
```
./context
```

### 3. ConfigMap
The following command creates the ConfigMap which contains non-sensitive environment variables:
```
kubectl apply -f configmap.yaml
```

### 4. ReplicaSet (optional)
This step is optional, you can skip to the next one.
To create the ReplicaSet:
```
kubectl apply -f replicaset.yaml
```

### 5. PersistentVolume & PersistentVolumeClaim
First you need to create the PersistentVolume via:
```
kubectl apply -f persistent-volume.yaml
```

Then you create the PersistentVolumeClaim which will bind to it:
```
kubectl apply -f persistent-volume-claim.yaml
```

### 6. Database
**First** set up the default database service and the Headless
```
kubectl apply -f postgres-service.yaml
kubectl apply -f postgres-headless-service.yaml
```

Then launch the statefulset:
```
kubectl apply -f postgres-statefulset.yaml
```

You can check the StatefulSet and the Pod that have been created using the following commands respectively:
```
kubectl get statefulset
kubectl get pod
``` 

### 7. Backend
First create the backend Service by running:
```
kubectl apply -f backend-service.yaml
```

You can confirm it has been created through:
```
kubectl get svc
```

Then create the backend Deployment by running
```
kubectl apply -f backend-deployment.yaml
```

### 8. Frontend
Run the following to create the frontend Service:
```
kubectl apply -f frontend-service.yaml
```

Then run the following to create the frontend Deployment:
```
kubectl apply -f frontend-deployment.yaml
```

Once you have confirmed all pods are up and running, obtain the URL of the node serving the application:
```
minikube service frontend-svc --url
```

You can access the app on the given URL.

### 9. Cleaning up
Run the following commands in order to gracefully delete the resources:
```
kubectl delete -f frontend-deployment.yaml 
kubectl delete -f backend-deployment.yaml 
kubectl delete -f postgres-statefulset.yaml 
kubectl delete -f postgres-service.yaml 
kubectl delete -f postgres-headless-service.yaml 
kubectl delete -f backend-service.yaml 
kubectl delete -f frontend-service.yaml 
kubectl delete -f persistent-volume-claim.yaml 
kubectl delete -f persistent-volume.yaml 
kubectl delete -f configmap.yaml 
kubectl delete -f namespace.yaml 
```
