# StatefulSet Problem
    StatefulSet provides stable pod identities, stable network names, persistent storage association, and ordered deployment/scaling for stateful applications such as MongoDB, PostgreSQL, Kafka, and Cassandra.
    
    This file yml is similar like deployment.yml
    StatefulSet exists because Deployment is not suitable for stateful applications like databases.

## First Understand the Problem
    Suppose MongoDB runs as a Deployment.
    Deployment
    |
     +--> mongo-pod

    Everything works. Now Pod crashes. Kubernetes creates: -> mongo-pod-abc123
    New Pod: -> mongo-pod-xyz456

## Problems:
Problem 1: Pod name changes
    mongo-pod-abc123 -> becomes mongo-pod-xyz456
    Not stable.

Problem 2: Network identity changes
    IP changes.-> 10.244.0.5
    becomes -> 10.244.0.12

Problem 3: Storage association
    If multiple replicas exist:
    mongo-pod-1
    mongo-pod-2
    mongo-pod-3

    How do you ensure each pod gets its own disk? Deployment doesn't guarantee that.

# Why StatefulSet Was Created

    For applications that need:

    ✅ Stable identity
    ✅ Stable hostname
    ✅ Stable storage
    ✅ Ordered startup/shutdown

    Examples: MongoDB, MySQL, PostgreSQL, Cassandra, Kafka, Elasticsearch, Redis Cluster, ZooKeeper

## Deployment vs StatefulSet

#Deployment: Pods are interchangeable.
#StatefulSet : Each pod has an identity.
    mongo-0
    mongo-1
    mongo-2

    Names never change.
# Example
    Create:

    kind: StatefulSet
    metadata:
        name: mongo
    
    Kubernetes creates:
    mongo-0
    mongo-1
    mongo-2

    Always.Even after restart:

    mongo-0
    mongo-1
    mongo-2

    still same names.

# Stable DNS
#Deployment:backend-abc123
            backend-xyz456
            unpredictable.

#Deployment:
            mongo-0.mongo-headless
            mongo-1.mongo-headless
            mongo-2.mongo-headless

          always available.
             

# When NOT to Use StatefulSet
#Don't use StatefulSet for:
Frontend
Backend API
Nginx
React
Next.js
Spring Boot API
Node.js API

# Note: These are stateless. Use Deployment.