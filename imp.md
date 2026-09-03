# Note:
In a Deployment YAML file, we define the desired state of Pods, including the Pod template and the application/container specifications. In a Pod YAML file, we directly define the specifications of the Pod and its containers.


# Simple way to remember
**Deployment → manages Pods**

    Deployment
    ↓
    Pod
    ↓
    Container
    ↓
    Application