# Pod Creation
    > kubectl apply -f pod.yml

# Verify Pods 
    > kubectl get pods

# Chekc All Pods 
    > kubectl get pods -n name_space

# Pods Describe in details
    > kubectl describe pod pod_name -n namesapce_name

# SSH into Pods
    > kubectl exec -it pod_name -- /bin/sh

# Pod Log Check
    Some time suppose pods runs and internally getting DB connection failed or something else so to check we use log.

    > kubectl logs nginx-pod

# Check Which Worker Got It?
    Means Sometime i want to check this pods is running in which Worker Node

    > kubectl get pods -o wide


