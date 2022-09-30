# Kubernetes  - PODs
### Get Worker Nodes Status
- Verify if kubernetes worker nodes are ready. 
```
# Configure Cluster Creds (kube config) for Azure AKS Clusters
az aks get-credentials --resource-group <resource group name> --name <cluster name>

# Get Worker Node Status
kubectl get nodes

# Get Worker Node Status with wide option
kubectl get nodes -o wide
```

### Create a Pod
- Create a Pod
```
# Template
kubectl run <desired-pod-name> --image <Container-Image> 
```  

### List Pods
- Get the list of pods
```
# List Pods
kubectl get pods

# Alias name for pods is po
kubectl get po

# List pods with wide option which also provide Node information on which Pod is running
kubectl get pods -o wide
```

### Describe Pod
- Describe the POD, primarily required during troubleshooting. 
- Events shown will be of a great help during troubleshooting. 
```

# Describe the Pod
kubectl describe pod <pod-name>
```

### Delete Pod
```
# Delete Pod
kubectl delete pod <pod-name>
```

## Expose Pod with a Service
- Expose pod with a service (Load Balancer Service) to access the application externally (from internet)
- **Ports**
  - **port:** Port on which node port service listens in Kubernetes cluster internally
  - **targetPort:** We define container port here on which our application is running.
- Verify the following before LB Service creation
  - Azure Standard Load Balancer created for Azure AKS Cluster
    - Frontend IP Configuration
    - Load Balancing Rules
  - Azure Public IP 
```
# Expose Pod as a Service
kubectl expose pod <pod-name>  --type=LoadBalancer --port=80 --name=<Service-Name>

# Get Service Info
kubectl get service
kubectl get svc

# Describe Service
kubectl describe service <service name>

# Access Application via external port
http://<External-IP-from-get-service-output>
```
- Verify the following after LB Service creation
  - Azure Standard Load Balancer created for Azure AKS Cluster
    - Frontend IP Configuration
    - Load Balancing Rules
  - Azure Public IP
- View the resources in Azure AKS Cluster - Resources section from Azure Portal Management Console  

### Verify Pod Logs
```
# Dump Pod logs
kubectl logs <pod-name>

# Stream pod logs with -f option and access application to see logs
kubectl logs -f <pod-name>
```
- **Important Notes**
  - Refer below link and search for **Interacting with running Pods** for additional log options
  - Troubleshooting skills are very important. So please go through all logging options available and master them.
  - **Reference:** https://kubernetes.io/docs/reference/kubectl/cheatsheet/

### Connect to Container in a POD
- **Connect to a Container in POD and execute commands**
```
# Connect to Nginx Container in a POD
kubectl exec -it <pod-name> -- /bin/bash
 
# Execute some commands in Nginx container
ls
cd /usr/share/nginx/html
cat index.html
exit
```

- **Running individual commands in a Container**
```
kubectl exec -it <pod-name> -- env

# Sample Commands
kubectl exec -it <pod-name> -- env
kubectl exec -it <pod-name> -- ls
kubectl exec -it <pod-name> -- cat /usr/share/nginx/html/index.html
```

### Get YAML/JSON Output
```
# Get pod definition YAML output
kubectl get pod <pod-name> -o yaml   
[or]
kubectl get pod <pod-name> -o json

# Get service definition YAML output
kubectl get service <service-name> -o yaml   
[or]
kubectl get service <service-name> -o json
```

##  Clean-Up
```
# Get all Objects in default namespace
kubectl get all

# Delete Services
kubectl delete svc <service-name>

# Delete Pod
kubectl delete pod <pod-name>

# Get all Objects in default namespace
kubectl get all
```