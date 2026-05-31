# Deployment 
    Basically hamare pods ko autoheal, desired state aur jab launch ho pod toh kon sa template use kare yehi sab toh define hota hai.

    Jab Deployment banta hai toh ham ukse metadata me sabse pahele uska name aur kon se namesapce me rhega o batate hain like this.
    metadata:
        name: portfolio-deployment
        namespace: portfolio

## Selector : 
    selector:
        matchLabels:
        app: portfolio   

    meaning deployment bol rha muhe o sare pods dhundho jinpar level hai.
    app: portfolio


## Real Problem
    Maan lo Deployment ne 3 Pods create kiye:
    pod-1
    pod-2
    pod-3
    Ab Deployment ko kaise pata chalega:
    Kaunse Pods mere hain?
    Kubernetes ko koi magic nahi pata.
    Usko ek identity chahiye.

    Ex - Labels = Name Tag
    Imagine school me bachchon ko tag lagaya:
    Name: Rahul
    Class: 10A
    
    Ya company me:
    Department: DevOps


## Template :
    first understand why we define template. basically we know that deployment me ham replica number change kar k 0 or 10 or kuch bhi karte hai toh uske accroding pods start hote, create hote right. but un pods ko start hone ke liye create hone ke liye koi toh template chahiye right. toh ham template me a batate hain ki jo bhi new pods create ho usme auto labels lag jaye portfolio ka.

    template: 
    metadata: 
      labels:
        app: portfolio

## Spec: 
    Jab Pods Creeate hoga toh uska kuch specification bhi toh rhena chahiye.

    spec: 
      containers: 
      - name: portfolio-container
        image: shivamsdeng/my-portfolio:v1

        ports:
        - containerPort: 3000
