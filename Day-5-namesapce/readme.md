# namespaces :
    In Kubernetes, namespaces provide a mechanism for isolating groups of resources within a single cluster. 

### Why Do We Use Namespaces?
    1. Resource Isolation : Team A should not see Team B resources.
    2. Access Control : Using RBAC, we can say:
        Shivam -> Team-A only
        Rahul -> Team-B only
    3. Resource Quotas
        Example:
        Team-A -> Max 10 CPU
        Team-B -> Max 20 CPU

![My Screenshot](1.png)

# What Problem Does Namespace Solve?
    Imagine your kind cluster hosts:

## Banking Application
    > nginx
    > mysql
    > backend
## E-commerce Application
    > nginx
    > postgres
    > frontend

## Without namespaces:
    frontend
    backend
    mysql
    frontend
    backend
    mysql

Name conflicts. Confusion. Permissions become difficult.
Problem: Two nginx deployments, Two services, Multiple teams
How do we separate them? : Namespace solves this.
Think of Namespace as: Folder inside Kubernetes.

## With namespaces:
    banking
    │
    ├── frontend
    ├── backend
    └── mysql

    ecommerce   
    │
    ├── frontend
    ├── backend
    └── mysql



![My Screenshot](2.png)




# Create Namespace
    > kubectl create namespace dev

![My Screenshot](3.png)



    > kubectl get ns

# Deploy into Namespace
    > kubectl create deployment nginx --image=nginx -n dev
    > kubectl get pods -n dev

