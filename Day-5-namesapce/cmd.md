# Check Existing Namespace 
    > kubectl get ns

# Create Namespace 
    numebr 1: Either run direct this command 
    > kubectl create namespace development

    Or File Based Create Namespace
    > kubectl apply -f namespace.yml

# Make it Default Namespace
    > kubectl config set-context --current --namespace=development

    Verify: 
    > kubectl config view --minify


## Problem:
    Everytime we have to define in which namesapce you are looking your resource. suppose i am looking total number of pods running in development.

    > kubectl get pods -n development

    an i need to check multiple things always in development so i have to mention -n namespace always. better to set the defaul this one.


