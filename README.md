
# Ghost Blog Kubernetes Deployment on GKE

This repository contains the Kubernetes configuration files for deploying the Ghost blogging platform on Google Kubernetes Engine (GKE). The setup includes a MySQL database for Ghost, a Nginx reverse proxy, as well as necessary ConfigMaps and Secrets.

## Prerequisites

-   A working Google Kubernetes Engine (GKE) cluster.
-   `kubectl` command-line tool installed.
-   `kubectl` configured to communicate with your GKE cluster.
-   Necessary permissions to deploy services and other resources on the cluster.


## Deployment Steps

  

### 1. Configurations and Secrets

Before deploying any components, we need to set up the necessary configurations and secrets:


    kubectl create  configmap  nginx-config  --from-file=nginx-config.conf 

#Creates  an  Nginx  config  map  from  the local  configuration  file

    kubectl create  secret  tls  ghost-tls-secret  --cert=mycert.crt  --key=private.key
#Creates  a  Kubernetes  secret  for Ghost's TLS.
    
    kubectl apply  -f  k8s/configMap.yaml
#Applies a ConfigMap, decoupling environment-specific configuration.
    
    kubectl apply  -f  k8s/secret.yaml
#Applies a Secret, intended for sensitive information.
  

  

### 2. MySQL Database

Set up the MySQL database which the Ghost blog will use:

    kubectl apply -f k8s/mysql/mysql-pvc.yaml
   #Creates a PVC for MySQL.
    
    kubectl apply -f k8s/mysql/mysql-service.yaml
   #Creates a Service for MySQL.
    
    kubectl apply -f k8s/mysql/mysql-dep.yaml
   #Deploys the MySQL pod.


### 3. Nginx Reverse Proxy

Deploy the Nginx reverse proxy:


    kubectl apply -f k8s/nginx/nginx-config.conf
   #Applies the Nginx configuration.
    
    kubectl apply -f k8s/nginx/nginx-service.yaml
   #Creates a Service for Nginx.
    
    kubectl apply -f k8s/nginx/nginx-deployment-sec.yaml
   #Deploys the Nginx pod with security configurations.
  

### 4. Ghost Blog Application

Finally, deploy the Ghost blog:

    kubectl apply -f k8s/ghost/ghost-pvc.yaml
#Creates a PVC for Ghost.    
    
    kubectl apply -f k8s/ghost/ghost-service.yaml
#Creates a Service for Ghost.  
    
    kubectl apply -f k8s/ghost/ghost-dep.yaml
#Deploys the Ghost blog


## Verification

After applying the commands, ensure that all the pods, services, and other resources are running correctly:

    `kubectl get pods,services` 

This command lists the current pods and services. Ensure all pods are in the `RUNNING` state.

## Accessing the Ghost Blog

Once all resources are running, you can access the Ghost blog through the service IP or DNS name associated with the Nginx service.


## Documentation

[Documentation](https://asafahmadov.gitbook.io/hands-on-projects/)


## 🚀 About Me
I'm a DevSecOps engineer


## 🔗 Links

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/asaf-ahmadov/)


