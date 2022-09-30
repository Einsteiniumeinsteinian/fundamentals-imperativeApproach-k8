# Kubernetes - Services

## Step-01: Introduction to Services
- **Service Types**
  1. ClusterIp
  2. NodePort
  3. LoadBalancer
  4. ExternalName
  5. Ingress
- LoadBalancer Type is primarily for cloud providers and it will differ cloud to cloud, so we will do it accordingly (per cloud basis)

## ClusterIP Service - Backend Application Setup
- Create a deployment for Backend Application 
- Create a ClusterIP service for load balancing backend application. 
```
# Create Deployment for Backend Rest App
kubectl create deployment <deployment-name> --image=<image-name> 
kubectl get deploy

# Create ClusterIp Service for Backend Rest App
kubectl expose deployment <deployment-name> --port=8080 --target-port=8080 --name=<backend-service-name>
kubectl get svc
Observation: No need to specify "--type=ClusterIp" because default setting is to create ClusterIp Service. 
```
- **Important Note:** If backend application port (Container Port: 8080) and Service Port (8080) are same we don't need to use **--target-port=8080** 


## LoadBalancer Service - Frontend Application Setup
- Create a deployment for Frontend Application (Nginx acting as Reverse Proxy)
- Create a LoadBalancer service for load balancing frontend application. 
- **Important Note:** In Nginx reverse proxy, ensure backend service name `backend-service-name` is updated when you are building the frontend container.
- **Nginx Conf File**
** proxy_pass http://<backend-service-name>:<port>;**
```conf
server {
    listen       80;
    server_name  localhost;
    location / {
    # Update your backend application Kubernetes Cluster-IP Service name  and port below      
    # proxy_pass http://<Backend-ClusterIp-Service-Name>:<Port>;      
    proxy_pass http://<backend-service-name>:<port>;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

```
# Create Deployment for Frontend Nginx Proxy
kubectl create deployment my-frontend-nginx-app --image=<image-name>
kubectl get deploy

# Create LoadBalancer Service for Frontend Nginx Proxy
kubectl expose deployment my-frontend-nginx-app  --type=LoadBalancer --port=80 --target-port=80 --name=<service-name>
kubectl get svc

# Get Load Balancer IP
kubectl get svc
http://<External-IP-from-get-service-output>

# Scale backend with 10 replicas
kubectl scale --replicas=10 deployment/<deployment-name>

# Test again to view the backend service Load Balancing
http://<External-IP-from-get-service-output>
```
