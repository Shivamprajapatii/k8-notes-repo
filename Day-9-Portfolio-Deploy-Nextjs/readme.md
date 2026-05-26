# Deploy Real App
    In this tutorial we will deploy a real application. 

### Step 1: first clone the app in the Server
    > git clone repo_name

## Creaet Dockerfile in the Application and then Create Image
Create Dockerfile based on the application it can be nextjs, node, flask or anything.

    > docker build -t my-portfolio:v1 .
    > docker images
    > docker run -d -p 3000:3000 --name portfolio my-portfolio:v1  

    Run and test locally

### Step 2: Push Image on The Docker Hub
    > docker tag portfolio:v1 shivamsdeng/portfolio:v1
    > docker login
    > docker push shivamsdeng/portfolio:v1

