Working with Kubernetes Nodes
Kubernetes Nodes
Now that we have our minikube cluster setup, let's dive into nodes in kubernetes.

What Is a Node
In Kubernetes, think of a node as a dedicated worker, like a dependable employee in an office, responsible for executing tasks and hosting containers to ensure seamless application performance. A Kubernetes Node is a physical or virtual machine that runs the Kubernetes software and serves as a worker machine in the cluster. Nodes are responsible for running Pods, which are the basic deployable units in Kubernetes. Each node in a kubernetes cluster typically represents a single host system.

Managing Nodes in kubernetes:
Minikube simplifies the management of Kubernetes for development and testing purposes. But in the context of minikube (a kubernetes cluster), we need to start it up before we can be able to access our cluster.

Start Minikube Cluster:
minikube start

On Ubuntu Server (AWS)

StartMinikube

Kubernetes on Local Computer

StarsMinikubeonWindow

This command starts a local Kubernetes cluster (minikube) using a single-node Minikube setup. It provisions a virtual machine (VM) as the Kubernetes node.

Stop Minikube Cluster:
minikube stop

StopMinikube

Stops the running Minikube (local kubernetes cluster), preserving the cluster state.

Delete Minikube Cluster:
minikube delete

Deletes the Minikube kubernetes cluster and its associated resources.

View Nodes:
kubectl get nodes

On Window

GetNodes

On Ubuntu

OnUbuntu

Lists all the nodes in the kubernetes cluster along with their current status.

Inspect a Node:
kubectl describe node <node-name>

Provides detailed information about a specific node, including its capacity, allocated resources, and status.

On Windows

InspectNode

On Ubuntu Linux

InspectNode

Node Scaling and Maintenance:

Minikube, as it's often used for local development and testing, scaling nodes may not be as critical as in production environments. However, understanding the concepts is beneficial:

Node Scaling: Minikube is typically a single-node cluster, meaning you have one worker node. For larger, production-like environments.

Node Upgrades: Minikube allows you to easily upgrade our local cluster to a new Kubernetes version, ensuring that our development environment aligns with the target production version.

By effectively managing nodes in Minikube kubernetes cluster, we can create, test, and deploy applications locally, simulating a Kubernetes cluster without the need for a full-scale production setup. This is particularly useful for debugging, experimenting, and developing applications in a controlled environment.

End.