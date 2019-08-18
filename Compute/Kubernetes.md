# Kubernetes

- Platform for managing container workloads
    - Create containers first, then manage them with Kubernetes
    - Kubernetes handles:
        - Deplopyment
        - Scaling
        - Updates containers (new versions of an app)
        - Load Balancing
        - And more...
    - Invented and used by Google, open sourced in 2014

## Kubernetes management overhead

- Cloud infrastructure provisioning
- Setting up CA and TLS cert generation
- Setting up TLS Client Bootstrap and RBAC auth
- Configure load balancing
- Configure DNS
- Configure container network routes
- Bootstrap Kubernetes Workers
- etc..

## Kubernetes Engine (GKE)

- Managed Kubernetes service for container workloads
- Google handles OS management, Master node, scaling, health checks, replication controller, and all of above management overhead.
    - You just focus on your containers and Google will handle the rest.

### Summary

**Kubernetes** manages your containers, while **Kubernetes Engine** manages your **Kubernetes**

## Architecture

### Nodes

- **Nodes** - VM's that containers are hosted on
    - GCE instances
    - Can have many containers/pods on a single node
- **Node Pool** - Group of nodes
    - Inside a MIG
- **Cluster** - One or more node pools
- **Node Image** - The OS image for the nodes
    - Current options for Node Images on GKE:
        - Container Optimized OS
        - Ubuntu
        - Container-Optimized OS with containerd (cos_containerd) (beta)
    - **Not the same as container image**

### Pods

- Smallest deployable unit - **deployed onto Nodes**
- Pods are one or multiple containers grouped together
- Deploy one or more **Pods** to **Nodes**

### Container Image

- Not the same as Node Image
- Base image used in the container - independent of the node OS
    - Google best practise is to use Alpine Linux - very lightweight container image

## Interacting with GKE applications

- Direct commands or refer YAML/JSON files for complex configs
- Use both `gsutil` and `kubectl` commands

### gcloud vs kubectl

- gcloud = interact with direct GCP resources (GKE cluster, nodes, GCE, disks)
- kubectl = interact with application **on the nodes** (pods)
    - Deploy pods, scale pods, update pods

### Management Concepts

#### Stateful vs. Stateless Pods

- Stateless applications (pods) do not save state - **livestock**. They do not save important information on these pods.
- Stateful applications (pods) save data to persistent disks - **pets**
    - Client entered data is saved to server (persistent disk)
    - **Updating and scaling stateful pods is much more careful work**

#### Container Image Best Practice

- **Deplpyment Optimization**
    - Use light base image like **Alpine** - smaller deployments and smaller security surface
    - In a Dockerfile, order matters - Do not copy source files before installing dependencies, causes unnecessary reinstalls

Below is an example Dockerfile, this is a good example as apline is being used as the container image and dependencies are installed before source code is copied.

```Dockerfile
FROM alpine

RUN apt-get update && apt-get install -y python python-pip

COPY ./src
```

- **Reliable Container Deployments**
    - When working with apps that are continuously updated, there will be new versions in the registry all the time.
    - Tag different versions of container deployments with version number, not just *"latest"*
    - When pulling images (deployng from container registry into GKE), there are 2 pull policy options:
        - **ifNotPresent** - Skip pulling image if it already exists - this is best practice
        - **Always** - Force a pull of the image, regardless if that version is already there or not
