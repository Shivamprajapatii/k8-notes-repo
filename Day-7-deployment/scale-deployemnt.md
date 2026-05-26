# Get Deployment 
    > kubectl get deployment -n development
    list all the deployment in the development namesapce

# Scale Deployemnt 
    > kubectl scale deployment nginx-deployment -n development --replicas=10
    > watch kubectl get pods -n development

# Downgrade Deployment
    > kubectl scale deployment nginx-deployment -n development --replicas=1

### Note: 
    There is two ways to increase and descrease pods for nwo either go to deployment file and change the replica number or directly run the command with your desired state. Ex kubectl scale deployment nginx-deployment -n development --replicas=1

## Roling Updates ?? 
## Deploymnet Strategy in K8 
1) Rolling Update (Default) / Recreate  -> Built-in Strategies
## Advanced Strategies (Progressive Delivery)
2) Blue/Green Deployment
3) Canary Deployment
4) A/B Testing
5) Shadow (Mirror) Deployment


# Questions
1) How many Pods can create in a node 
2) How many nodes can have a k8 Cluster -> for now in my case i haev 4 Cluster


