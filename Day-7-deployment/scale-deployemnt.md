# Get Deployment 
    > kubectl get deployment -n development
    list all the deployment in the development namesapce

# Scale Deployemnt 
    > kubectl scale deployment nginx-deployment -n development --replicas=10
    > watch kubectl get pods -n development

# Downgrade Deployment
    > kubectl scale deployment nginx-deployment -n development --replicas=1

### Note: 
    There is two ways to increase and descrease pods for now either go to deployment file and change the replica number or directly run the command with your desired state. 
    
    Ex > kubectl scale deployment nginx-deployment -n development --replicas=1

## Roling Updates ?? 
    In Kubernetes, a rolling update is the default deployment strategy that gradually replaces old Pods with new ones to ensure zero downtime. Instead of taking down your entire application at once, Kubernetes incrementally updates instances in small batches. This guarantees that a portion of your application always remains online and ready to handle incoming user traffic during the upgrade process


## Deploymnet Strategy in K8 
    1) Rolling Update (Default) / Recreate  -> Built-in Strategies
## Advanced Strategies (Progressive Delivery)
    2) Blue/Green Deployment
    3) Canary Deployment
    4) A/B Testing
    5) Shadow (Mirror) Deployment


# Questions
1) How many Pods can create in a node 

    Answer: Different platforms establish different default and maximum limits to protect resource allocation:

    1) Vanilla Kubernetes: Defaults to 110 pods per node.Google Kubernetes Engine (GKE): Defaults to 110 but allows manual configuration up to 256 pods.
    2) Azure Kubernetes Service (AKS): Supports a configuration range between 30 and 250 pods per node.
    3) Red Hat OpenShift: Defaults to 250 pods per node, but can be scaled up to 500 on high-performance nodes.
    4) sAmazon EKS: Varies drastically (from 4 to over 700) based entirely on the specific Amazon EC2 instance type.

2) How many nodes can have a k8 Cluster -> for now in my case i haev 4 Cluster




# Core Constraints on Pod Capacity
Even if you change the settings, four main technical bottlenecks determine your true max pod count:


**IP Address Allocation:** 
    Each Pod requires a unique IP address. Kubernetes typically assigns a /24 CIDR block (256 IPs) per node. Because it needs extra padding to prevent IP overlap during upgrades, the system stops you at 110 pods

**Hardware Compute Capacity:** 
    Pods run on shared CPU and RAM. If your node runs out of physical memory or compute capacity, the scheduler will block new pods from deploying.

**System Resource Overhead:**
     The Kubelet, operating system, and container runtime require dedicated resources to stay alive. This "Kube-reserved" space reduces the actual space available to your applications.

**Storage Limits:**
     Running out of local ephemeral storage blocks new pod instantiation. Cloud providers also restrict the maximum number of persistent storage disks (like AWS EBS volumes) that can plug into one node


# Hindi 
    1) So Don't think ki you wrote maximum pods run 500 in a worker there is limitation first you will face challenges of IP Address you must increase your network CIDR range to provide enough underlying IP addresses

    2) Your Node Capacity Should be High like RAM, CPU

    3) Storage Should have engoug 