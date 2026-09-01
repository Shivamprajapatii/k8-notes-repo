    When we say "bottleneck", we mean: Something is limiting the performance, capacity, or ability of Kubernetes to schedule/run workloads.
    And a bottleneck can happen at different levels.

# 1. First understand the hierarchy
Keep this picture in mind:

                        K8s CLUSTER
                            │
                ┌──────────┴──────────┐
                │                     │
                Node 1                Node 2
                │                     │
            ┌─────┴─────┐         ┌─────┴─────┐
            │           │         │           │
        Pod         Pod       Pod         Pod
            │           │         │           │
        Container   Container  Container   Container
            │
            ↓
    Application

# 2. Node bottleneck
A Node is your worker machine. For example:

    EC2
    4 vCPU
    16 GB RAM


Suppose Pods consume:

    Pod 1 → 2 CPU + 4 GB RAM
    Pod 2 → 1 CPU + 4 GB RAM
    Pod 3 → 1 CPU + 6 GB RAM

Total:

    CPU = 4 vCPU
    RAM = 14 GB

You're almost full. Now another Pod asks for:

    2 CPU
    4 GB RAM

The Node doesn't have enough resources. So:

    Pod 4
    ↓
    Cannot be scheduled on Node

**That's a Node resource bottleneck.**

# 3. CPU bottleneck

Suppose:

    Node:
    8 CPU

Your applications consume:

    Pod A → 3 CPU
    Pod B → 3 CPU
    Pod C → 2 CPU

Total:

    8 CPU

CPU is now the limiting resource.

You might see:

    CPU utilization = 95–100%

**Your applications may become slow.**  

# 4. Memory bottleneck

Suppose:

    Node:
    16 GB RAM

Pods consume:

    Pod A → 6 GB
    Pod B → 5 GB
    Pod C → 4 GB

Total:

    15 GB

Now another application starts consuming memory. You can eventually get:

    OOM(Out Of Memory)

A container can be killed because the system doesn't have enough memory.

You may see:

    OOMKilled

**This is a serious bottleneck.**

# 5. Disk bottleneck
Your Node also has storage.

For example:

    EC2
    100 GB EBS

Applications generate:

    Logs
    Temporary files
    Container images
    Application data

Eventually:

    Disk = 95%

**Now you have a disk bottleneck.**

At 100%:

    Applications may fail
    Logs may stop
    Containers may fail
    Kubelet may have problems


# 6. Network bottleneck
Nodes have network capacity.

Imagine:

    Node
    ↓
    Network
    ↓
    100 Mbps


Your applications are generating:

    90 Mbps
    80 Mbps
    70 Mbps

You can saturate the available capacity. Then:

    Latency ↑
    Throughput ↓
    Packet drops ↑

**That's a network bottleneck.**

# 7. Pod bottleneck

A Pod itself can become a bottleneck. Suppose:

    Pod
    └── Node.js

Your Node.js application can process:

    1,000 requests/sec
    But traffic becomes:
    5,000 requests/sec
    One Pod can't handle it.

You can increase replicas:

    1 Pod
    ↓
    3 Pods

Now:

    Pod 1 → 1,000 req/s
    Pod 2 → 1,000 req/s
    Pod 3 → 1,000 req/s

Approximately:

    3,000 req/s

assuming the workload scales well. **This is why replicas exist.**

# 🏢 Cluster Bottlenecks

- **Control Plane Overload:** The API server slows down from too many requests.
- **etcd Storage Limits:** The database slows down if it exceeds 8GB.
- **IP Address Exhaustion:** The cluster runs out of IPs for new Pods.
- **Cloud Provider Quotas:** You hit CPU or storage limits set by AWS, Azure, or GCP.
- **CoreDNS Saturation:** DNS resolution fails due to high request volume.

# 💻 Node Bottlenecks 

- **CPU Throttling:** Pods slow down because the Node CPU is at 100%.
- **Memory Exhaustion (OOM):** The Node runs out of RAM and kills Pods to survive.
- **Disk I/O Bottlenecks:** Slow read/write speeds delay database and log operations.
- **Disk Space (Ephemeral Storage):** The Node fills up with logs and evicts Pods.
- **Kubelet Pod Limits:** A single Node cannot host more than its maximum allowed Pods (default is 110).
- **Network Bandwidth:** High traffic saturates the Node’s network card.

# 📦 Pod & Container Bottlenecks

- **Incorrect Resource Limits:** Setting CPU limits too low triggers heavy throttling.
- **Single-Threaded Code:** The app uses only one CPU core while others sit idle.
- **Application Connection Pools:** The app runs out of database or HTTP connections.
- **Storage IOPS:** Persistent volumes throttle application data processing.