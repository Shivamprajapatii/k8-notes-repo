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

