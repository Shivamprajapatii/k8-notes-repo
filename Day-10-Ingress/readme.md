# Ingress:
    Ingress is similar like Nginx but not exact nginx, Kubernetes Ingress is an API object that acts as a smart router, managing external access to services within a cluster.

    Ingress is a Kubernetes API object that defines HTTP and HTTPS routing rules for external traffic entering the cluster. It routes requests to Services based on hostnames or URL paths.

    Ingress = Rules

    Basically it build for microservice applications. internally uses nginx.
    Redirect to /payment, /profile or etc

# What is an Ingress Controller?
    A software that reads Ingress rules and routes traffic.

    Popular controllers:
    NGINX Ingress Controller
    Traefik
    HAProxy Ingress
    AWS Load Balancer Controller
