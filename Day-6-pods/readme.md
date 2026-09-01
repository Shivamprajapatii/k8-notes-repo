# Pods
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
- Pod is the Kubernetes unit that contains and manages one or more containers.

**Pod is not what "runs" your container. Pod is the Kubernetes unit/environment that groups and manages the container; the container runtime (such as containerd) is what actually creates and runs the container.**

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


# What does that Pod actually contain?
Suppose we create: nginx-pod

The resulting structure is roughly:

                    POD
            ┌─────────────────────┐
            │                     │
            │   Pod IP            │
            │   Network Namespace │
            │                     │
            │   Volumes           │
            │                     │
            │   Containers        │
            │      │              │
            │      ↓              │
            │   nginx             │
            │      │              │
            │      ↓              │
            │  nginx process      │
            │                     │
            └─────────────────────┘


# What happens if the Pod has 2 containers?
A pod can have one or more containers inside that.

For example:

    spec:
    containers:
        - name: app
        image: myapp:1.0

        - name: nginx
        image: nginx:latest
    

Now Kubernetes creates:

                    POD
                    │
            ┌─────────┴─────────┐
            │                   │
    App Container       Nginx Container
            │                   │
        app                  nginx
    

## Both containers share the Pod's network.

For example:

    Pod IP = 10.244.1.25

    App       → localhost:8080
    Nginx     → localhost:80

**They are two containers, but one Pod.**

# The best mental picture

                        WORKER NODE
    ┌──────────────────────────────────────────┐
    │                                          │
    │  kubelet                                 │
    │  containerd                              │
    │                                          │
    │       ┌──────────── POD ────────────┐    │
    │       │                             │    │
    │       │  Pod IP: 10.244.1.25        │    │
    │       │                             │    │
    │       │  Network namespace          │    │
    │       │                             │    │
    │       │  Volumes                    │    │
    │       │                             │    │
    │       │  ┌──────────────────────┐   │    │
    │       │  │ nginx container      │   │    │
    │       │  │                      │   │    │
    │       │  │ nginx process        │   │    │
    │       │  └──────────────────────┘   │    │
    │       │                             │    │
    │       └─────────────────────────────┘    │
    │                                          │
    └──────────────────────────────────────────┘

# So when you create a Pod, what do you finally get?
You get a running Kubernetes-managed workload environment, normally containing one or more containers, with things like:

**Pod**

- Pod identity/name
- Pod IP/network namespace
- container(s)
- volume mounts if configured
- environment/configuration
- resource limits/requests
- security context
- service-account identity
- lifecycle/health information