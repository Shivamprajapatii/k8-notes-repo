# HPA(Horizontal Pod Scale) 
    now befroe this i run this deployment command with replica=x then based on that my pods gets scale. who will do this manual scale and down. 

    for this HPA come into the picture based on the node data like cpu,ram,disk we can set scalling polocy.

# Download Metrics API in the Node 
    > kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# Edit the Deployment


# Now Verify 
    > kubectl top pod -n potfolio
    > kubectl top node