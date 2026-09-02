# 1. First: What is a "Master Node"?
    We Know that Entire K8s is Working on Only Master Node(Control Plane) and Worker Node. Master Node also Know as Controle Plane and We Know Node is Nothing But a VMs or Cloud Server(EC2), Physical Server. 

    Let's first Understand the Master Node and then We will deep dive into the Master Node Components. Forget the word master for a moment. A Kubernetes cluster has:


                    KUBERNETES CLUSTER
                            │
            ┌─────────────┴─────────────┐
            │                           │
        CONTROL PLANE               WORKER NODES
        "Brain"                     "Workers"
            │                           │
            │                       ┌───┴───┐
            │                       │       │
            │                     Node 1  Node 2
            │                       │       │
            │                      Pods    Pods


    The control plane's job is basically: "Understand the desired state of the cluster and make the cluster move toward that state."


# 2. What is inside the Control Plane? Core Control Plane Components
The main components are:

    CONTROL PLANE
    │
    ├── kube-apiserver             - The front-end, exposing the Kubernetes API to validate and configure data for cluster objects.
    ├── etcd                       - A consistent, highly-available key-value store serving as the single source of truth for all cluster data
    ├── kube-scheduler             - Selects the best worker node for new pods based on resource requirements and policies
    ├── kube-controller-manager    - Runs various controller processes to regulate the actual state of the cluster against the desired state
    │
    └── cloud-controller-manager (optional)

    These are the core control-plane components documented by Kubernetes.

**There are also things on the machine that aren't technically control-plane components but are necessary for the node itself:**

    Control Plane Node
    │
    ├── kubelet
    ├── container runtime
    │
    ├── kube-apiserver
    ├── etcd
    ├── kube-scheduler
    ├── kube-controller-manager
    │
    └── networking components
    │
    └── cloud-controller-manager (optional)

# 3. First understand the physical machine
Suppose you create an EC2 instance:

    AWS EC2
    Ubuntu
    8 CPU
    32 GB RAM

Initially it's just:

    EC2
    └── Ubuntu Linux

    It isn't Kubernetes yet.

Then you install/bootstrap Kubernetes components.:
Conceptually:


    EC2
    │
    └── Ubuntu
        │
        ├── kubelet
        ├── container runtime
        └── Kubernetes control-plane components
    

With kubeadm, the control-plane manifests are placed under:

    /etc/kubernetes/manifests/


# 4. The most interesting part: Static Pods
Since all these at then end run into a pod like etcd pod, apiserver pod etc 
With kubeadm, you normally have files like: 

    /etc/kubernetes/manifests/

    ├── etcd.yaml
    ├── kube-apiserver.yaml
    ├── kube-controller-manager.yaml
    └── kube-scheduler.yaml

    These are Static Pod manifests.


The kubelet watches that directory. So:

    /etc/kubernetes/manifests/
            │
            ├── etcd.yaml
            ├── kube-apiserver.yaml
            ├── kube-controller-manager.yaml
            └── kube-scheduler.yaml
                        │
                        ↓
                    kubelet
                        │
                        ↓
                container runtime
                        │
                        ↓
                Control-plane Pods
            


# 6. Now let's understand each component

## Component #1 — kube-apiserver

This is the front door of Kubernetes.

    Think:

                    Kubernetes
                        │
                API Server
                        │
        ┌─────────────┼─────────────┐
        │             │             │
    kubectl       Scheduler      Controllers


When you run:

    > kubectl get pods


your request goes to:

    kubectl
    ↓
    kube-apiserver



**Why does everything talk to API Server?**
Suppose you create:

    kubectl apply -f deployment.yaml

You aren't directly talking to:

    scheduler
    controller-manager
    kubelet
    etcd

Your request goes through:

    kubectl
    ↓
    API Server

    The API server validates and processes the API request and interacts with the cluster state.

## Component #2 — etcd

This is extremely important. **etcd is the Kubernetes database.**
For example, Kubernetes needs to know things like:


    Which Deployments exist?
    Which Pods exist?
    Which Nodes exist?
    Which Services exist?
    What replicas are desired?
    What configuration exists?

Conceptually:

    etcd
    │
    ├── Deployments
    ├── Pods
    ├── Services
    ├── Nodes
    ├── ConfigMaps
    ├── Secrets
    ├── ReplicaSets
    └── Cluster configuration/state


## Component #3 — kube-scheduler
Now suppose you create:

    replicas: 5

Kubernetes needs to decide:

    "Where should these Pods run?" That's the scheduler's job.

Imagine:

    New Pod
    │
    ↓
    Scheduler
    │
    ├── Node 1 ❌
    ├── Node 2 ✓
    └── Node 3 ❌
            │
            ↓
        Node 2
    

**It considers things such as:**

    CPU
    Memory
    Node availability
    Taints/tolerations
    Affinity
    Anti-affinity
    Hardware requirements
    Policies
    Data locality

So: **Scheduler = "Where should this Pod run?"**

## Component #4 — kube-controller-manager
This one is slightly harder. The controller manager contains multiple controllers.

    Think of a controller as:
    A loop that continuously compares desired state with actual state and tries to make them match.


## Component #5 — cloud-controller-manager
This one is optional.
**If Kubernetes is running in a cloud environment, the cloud controller manager integrates Kubernetes with the underlying cloud provider.**

For example, in AWS, cloud integration can involve things like:

    AWS
    │
    ├── Load Balancers
    ├── Nodes/instances
    ├── Routes
    └── Cloud provider integration
