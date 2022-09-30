# Kubernetes - ReplicaSets
## Tasks
- Create ReplicaSet
- View ReplicaSet Description
- Test Replicaset Reliability or High Availability 
- Test ReplicaSet Scalability feature
- Expose ReplicaSet as a Service
- Delete Service created for ReplicaSet
- Delete ReplicaSet

### Create ReplicaSet
- Create ReplicaSet
```
kubectl create -f <file-name>
```
- **eg: file-name: replicaset.yml**

### List ReplicaSets
- Get list of ReplicaSets
```
kubectl get replicaset
kubectl get rs
```

### Describe ReplicaSet
- Describe the newly created ReplicaSet
```
kubectl describe rs/<replicaset-name>
[or]
kubectl describe rs <replicaset-name>
```


### Verify the Owner of the Pod
- Verify the owner reference of the pod.
- Verify under **"name"** tag under **"ownerReferences"**. We will find the replicaset name to which this pod belongs to. 
```
kubectl get pods <pod-name> -o yaml
```
### View ReplicaSet Description
```
kubectl get rs <replicaset-name> -o yaml
[or]
kubectl get rs <replicaset-name> -o json
```

## Expose ReplicaSet as a Service
- Expose ReplicaSet with a service (Load Balancer Service) to access the application externally (from internet)
```
# Expose ReplicaSet as a Service
kubectl expose rs <ReplicaSet-Name>  --type=LoadBalancer --port=80 --target-port=8080 --name=<Service-Name>

# Get Service Info
kubectl get service
kubectl get svc

```
- **Access the Application using External or Public IP**
```
http://<External-IP-from-get-service-output>/hello
```

## Test Replicaset Reliability or High Availability 
- Test how the high availability or reliability concept is achieved automatically in Kubernetes
- Whenever a POD is accidentally terminated due to some application issue, ReplicaSet should auto-create that Pod to maintain desired number of Replicas configured to achive High Availability.
```
# To get Pod Name
kubectl get pods

# Delete the Pod
kubectl delete pod <Pod-Name>

# Verify the new pod got created automatically
kubectl get pods   (Verify Age and name of new pod)
``` 

## Test ReplicaSet Scalability feature 
- Test how scalability is going to seamless & quick
- Update the **replicas** field in **replicaset.yml** from 3 to 6.
```
# Before change
spec:
  replicas: 3

# After change
spec:
  replicas: 6
```
- Update the ReplicaSet
```
# Apply latest changes to ReplicaSet
kubectl replace -f replicaset.yml

# Verify if new pods got created
kubectl get pods -o wide
```

### Delete ReplicaSet
```
# Delete ReplicaSet
kubectl delete rs <ReplicaSet-Name>
[or]
kubectl delete rs/<ReplicaSet-Name>

# Verify if ReplicaSet got deleted
kubectl get rs
```

### Delete Service created for ReplicaSet
```
# Delete Service
kubectl delete svc <service-name>
kubectl delete svc/<service-name>

# Verify if Service got deleted
kubectl get svc
```
