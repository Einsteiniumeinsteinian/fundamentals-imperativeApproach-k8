# Kubernetes - Deployment
## Tasks
- Create a Deployment
- Scale the Deployment
- Expose the Deployment as a Service

## 01 Create Deployment
- Create Deployment to rollout a ReplicaSet
- Verify Deployment, ReplicaSet & Pods
- **Example Docker Image Location:** https://hub.docker.com/repository/docker/stacksimplify/kubenginx
```
# Create Deployment
kubectl create deployment <Deployment-Name> --image=<Container-Image:version>

# Verify Deployment
kubectl get deployments
kubectl get deploy 

# Describe Deployment
kubectl describe deployment <deployment-name>

# Verify ReplicaSet
kubectl get rs

# Verify Pod
kubectl get po
```
## 02 Scaling a Deployment
- Scale the deployment to increase the number of replicas (pods)
```
# Scale Up the Deployment
kubectl scale deployment <Deployment-Name> --replicas 1
[or]
kubectl scale --replicas=10 deployment/<Deployment-Name> 

# Verify Deployment, Pods and Replicaset
kubectl get deploy, kubectl get rs, kubectl get po
```

# 03 Expose Deployment as a Service (LoadBalancer Service) to access the application externally (from internet)

kubectl expose deployment <Deployment-Name>  --type=LoadBalancer --port=80 --target-port=80 --name=<Service-Name-To-Be-Created>

# Get Service Info
kubectl get svc
```
- **Access the Application using Public IP**
```
http://<External-IP-from-get-service-output>
```