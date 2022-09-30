# Rollback Deployment

### Check the Rollout History of a Deployment
```
# List Deployment Rollout History
kubectl rollout history deployment/<Deployment-Name>
```

### Verify changes in each revision
- **Observation:** Review the "Annotations" and "Image" tags for clear understanding about changes.
```
# List Deployment History with revision information
kubectl rollout history deployment/<Deployment-Name> --revision=<revision-number>
```

### Rollback to previous version
```
# Undo Deployment
kubectl rollout undo deployment/<Deployment-Name> 
```

### Rollback to specific revision
```
# Rollback Deployment to Specific Revision
kubectl rollout undo deployment/<Deployment-Name> --to-revision=3
```

## Rolling Restarts of Application
- Rolling restarts will kill the existing pods and recreate new pods in a rolling fashion. 
```
# Rolling Restarts
kubectl rollout restart deployment/<Deployment-Name>
```

### List Deployment Rollout History
```
kubectl rollout history deployment/<Deployment-Name>   
```

### Verify Deployment, Pods, ReplicaSets
```
kubectl get deploy
kubectl get rs
kubectl get po
kubectl describe deploy <Deployment-Name>
```

### Access the Application using Public IP
```
# Get Load Balancer IP
kubectl get svc

# Application URL
http://<External-IP-from-get-service-output>
```

