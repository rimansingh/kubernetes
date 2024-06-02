# Install Kubernetes

### You must ensure you have at least two servers or VMs.
### 1. Master
### 2. Worker

## ----- Install below commands on both machines [Master and Worker] -----

## Step 1: Install Docker

      sudo apt-get update
      sudo apt-get install -y docker.io
      sudo usermod -aG docker ${USER}
      sudo systemctl enable docker
      sudo systemctl start docker

## Install kubeadm, kubelet, kubectl

      sudo apt-get update -y
      sudo apt-get install -y apt-transport-https ca-certificates curl gpg
      curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
      echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

      sudo apt-get update
      sudo apt-get install -y kubelet kubeadm kubectl
      sudo apt-mark hold kubelet kubeadm kubectl

## Disable swap

      sudo swapoff -a
      sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
      

## ----- Install below commands only on Master -----

## Initialize the Kubernetes cluster
      sudo kubeadm init --apiserver-advertise-address=192.168.56.20 --pod-network-cidr=10.244.0.0/16

## Set up kubeconfig for the vagrant user
      mkdir -p $HOME/.kube
      sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
      sudo chown $(id -u):$(id -g) $HOME/.kube/config

## Apply Flannel CNI plugin
      kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
      
      kubeadm token create --print-join-command

## Configure the required ports for Kubernetes communication
      sudo ufw allow 6443/tcp  # Kubernetes API server
