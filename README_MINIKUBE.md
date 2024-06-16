### Start Minikube with Docker driver
    minikube start --force --driver=docker

# Check Docker containers
docker ps
docker ps -a

# Check Docker images
docker images

# Check Minikube status
minikube status

# Create a deployment with nginx image
kubectl create deployment my-nginx --image=nginx

# Check the status of the deployment and pods
kubectl get deployment
kubectl get pods

# Expose the deployment to access it via NodePort
minikube kubectl -- expose deployment my-nginx --type=NodePort --port=80

# Get the service URL from Minikube
minikube service my-nginx

# Verify the service is running using curl (replace with your actual URL)
curl http://192.168.49.2:32169

# Forward a local port to the service port without using sudo
kubectl port-forward --address=0.0.0.0 service/my-nginx 30618:80

