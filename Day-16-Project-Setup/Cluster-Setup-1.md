# Context:
    Today I will learn and deploy end to end project in EC2 K8 Cluset.

# Step 1: Setup Server 
    First i launched a fresh Server and did ssh and did 
    > sudo apt update
    > sudo apt upgrade

# Software Installation 
    > sudo apt-get install docker.io
    > docker -v 
    > sudo usermod -aG docker ubuntu
    > newgrp docker

# Install Kind 
    > [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
    > ls
    > chmod +x ./kind
    > ./kind --version
    > sudo mv ./kind /usr/local/bin/kind
    > kind --version 

# Insall Kubectl 
    > curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    > ls
    > chmod +x ./kubectl
    > ./kubectl version
    > sudo mv ./kubectl /usr/local/bin/kubectl

    > kubectl version

# Create Kind Cluster   

    > mkdir kind-cluster
    > cd kind-cluster
    > sudo vi cluster.yml

# Edit and Write thsi
    kind: Cluster
    apiVersion: kind.x-k8s.io/v1alpha4

    nodes:
    - role: control-plane
    image: kindest/node:v1.31.2

    - role: worker
    image: kindest/node:v1.32.2

    - role: worker
    image: kindest/node:v1.32.2

    - role: worker
    image: kindest/node:v1.32.2
