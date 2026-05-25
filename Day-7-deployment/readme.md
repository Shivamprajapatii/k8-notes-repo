# Deployments
    A Deployment is a Kubernetes object that manages Pods.
    A Kubernetes Deployment is a high-level resource object that manages the lifecycle of your applications by defining their "desired state".

# Problem 
    You currently have:
    development
    │
    └── nginx Pod
    You created a Pod directly. Problem: If the Pod dies:
    kubectl delete pod nginx -n development

    It's gone. Kubernetes will NOT recreate it.
    Why? Because you only told Kubernetes: "Create one Pod." You never told Kubernetes:
    "Always keep one nginx running."

# Real Requirement
    Usually we want: I want 3 nginx Pods running all the time. or If one crashes, create another. or Upgrade nginx version without downtime.
    A Pod cannot do these things. That's where Deployment comes in.

# What is a Deployment?
    Think of Deployment as a manager for Pods. Deployment doesn't run containers. Pods run containers. Deployment manages Pods.
    Deployment
      ↓
    ReplicaSet
      ↓
    Pods

# You can verify later:
    > kubectl get deployments
    > kubectl get replicasets
    > kubectl get pods



