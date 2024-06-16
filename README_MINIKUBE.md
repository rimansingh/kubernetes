# Setting Up Minikube with Docker and Deploying an Nginx Application

## Prerequisites
### Ensure you have a virtual machine and Docker installed on your system.


## Step 1: Start Minikube with Docker driver
    minikube start --force --driver=docker

## Step 2:  Check Docker containers
    docker ps
    docker ps -a

## Step 3: Check Docker images
    docker images

# Step 4: Check Minikube status
    minikube status

# Step 5: Create a deployment with nginx image
    kubectl create deployment my-nginx --image=nginx

# Step 6: Check the status of the deployment and pods
    kubectl get deployment
    kubectl get pods

# Step 7: Expose the deployment to access it via NodePort
    minikube kubectl -- expose deployment my-nginx --type=NodePort --port=80

# Step 8: Get the service URL from Minikube
    minikube service my-nginx

# Step 9: Verify the service is running using curl (replace with your actual URL)
    curl http://192.168.49.2:32169

# Step 10: Forward a local port to the service port without using sudo
    kubectl port-forward --address=0.0.0.0 service/my-nginx 30618:80

