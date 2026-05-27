# Kubectl Command Deep Dive 
    kubectl is the command-line client for Kubernetes. It is how you ask the cluster to show, create, change, or inspect things.

## get Commmand
    > kubectl get namespaces
    > kubectl get deployments
    > kubectl get pods
    > kubectl get nodes
    > kubectl get service

If we want something from our cluster we use get command.  

## describe Commmand: Shows full details of one object.
    > kubectl describe pod nginx
    > kubectl describe node first-cluster-worker

## delete Commands:
    > kubectl delete pod nginx
    > kubectl delete -f nginx.yaml

## apply Command
    > kubectl apply -f nginx.yaml

## Command Which Pod is Running on Which Cluster Node
    > kubectl get pods -n portfolio -o wise

## Get all thing in a signle Command which come under a Namesapce 
    > kubectl get all -n portfolio
     