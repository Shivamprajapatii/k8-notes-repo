# ConfigMap
    ConfigMap is another core Kubernetes object that solves a very common problem:
    How do I give configuration to my application without hardcoding it inside the Docker image?

    Problem Without ConfigMap. Suppose your Node.js app has:
    const DB_HOST = "mongodb.prod.internal";
    const PORT = 3000;

    You build the image:> docker build -t wonderlust:v1 .
    Now tomorrow:
    DB_HOST changes
    PORT changes
    API_URL changes

You would need to:

    Change code
        ↓
    Build image again
        ↓
    Push image
        ↓
    Deploy again

Bad practice.