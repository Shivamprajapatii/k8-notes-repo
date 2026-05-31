# Persistent volume kubernetes
    as in docker when we run db and suddnly we stop or delete the container then our entire data goes deleted. same in k8 also if pods get deleted then all data will go forever.

    for this Persistent volume concept come which used to store the data seperetlly if pods gets delted data will stay persitent.

# Note: 
    sotrage will create in the worked node not in master or control plan.


# Apply Commnad 
    > kubectl apply -f persistant.yml
    > kubectl get pv 

# Claim Volum with Pod
    persitent volume is create it is available now but now you will have to map that with pods

    write again a persitent volume claim file .yml

    > kubectl apply -f persitentVolumeClaim.yml
    
