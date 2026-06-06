# Beginer Proble:
    SUppose i Created Kind Cluster with cluster.yml using this command > kind create cluster --config cluster.yml --name first-cluster

    -> Now after that we want to destroy are delete cluster or nodes either at a time or one by one

# Number of Was to Delete Kind Cluter
    1. Delete the Entire Kind Cluster (Most Common)
    > kind get clusters
    > kind delete cluster --name my-cluster

    2. Delete Docker Containers Manually
    > docker ps -a
    > docker rm -f kind-control-plane kind-worker kind-worker2 kind-worker3


    3. Delete the Kubernetes Resources but Keep the Cluster
    > kubectl delete all --all -n name-space-name

    Delete namespace:
    > kubectl delete namespace wonderlust-prod
    Cluster remains running.

# Delete All Clutser Command 
    > kind delete cluster --name my-cluster


# Verify Nothing Remains    
    > kind get clusters

    
# Why does kind delete cluster work?
    First things kind creates the cluster after that kubectl access those. cluster ware build using kind not with kubectl.

# Real AWS Example
    Suppose you have an EKS cluster:
    AWS
    └── EKS Cluster

    You can do: > kubectl delete pod nginx
    
    But you cannot do: > kubectl delete cluster eks-prod


# because Kubernetes does not manage itself.
    Instead AWS manages the cluster.
    You would use:
    > aws eks delete-cluster --name eks-prod

