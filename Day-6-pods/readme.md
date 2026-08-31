# Pods
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
- Pod is the Kubernetes unit that contains and manages one or more containers.

# Docker run time vs Pods Runtime 

             NORMAL
               │
             Docker
               │
               ↓
           Container
               │
               ↓
          Application




            KUBERNETES
               │
           Kubernetes
               │
               ↓
              Pod
               │
               ↓
        Container Runtime
       (containerd / CRI-O)
               │
               ↓
           Container
               │
               ↓
          Application