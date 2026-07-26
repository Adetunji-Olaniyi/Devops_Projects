Setup Prometheus Node Exporter on Kubernetes
Introduction
Prometheus is a widely-used monitoring system that collects and processes metrics from various sources. The Node Exporter is a Prometheus exporter that collects hardware and operating system metrics from a system. By deploying Node Exporter on Kubernetes, you can monitor the nodes in your Kubernetes cluster and gain insights into their performance.

Objectives
Understand the purpose of Prometheus Node Exporter.
Deploy Node Exporter as a DaemonSet in a Kubernetes cluster.
Configure Prometheus to scrape metrics from Node Exporter.
Visualize metrics using Prometheus UI. Explore metrics available through Node Exporter.
Prerequisites
Kubernetes Cluster: A working Kubernetes cluster (e.g., Minikube, Kind, or a managed kubernetes service like EKS or AKS or GKE).
Kubernetes CLI: kubectl installed and configured for your cluster.
Prometheus Setup: Basic Prometheus installation running in the Kubernetes cluster.
Tools: A text editor to modify YAML files.
Tasks Outline
Understand how Node Exporter works and its purpose.
Deploy Node Exporter as a DaemonSet.
Configure Prometheus to scrape metrics from Node Exporter.
Verify the metrics in Prometheus.
Explore the metrics provided by Node Exporter.
Project Tasks
Task 1 - Understand How Node Exporter Works
Node Exporter is a lightweight application that runs on a node and exposes metrics about the node’s hardware and operating system.
Key metrics include:
CPU and memory usage
Disk I/O
Network statistics
Filesystem usage
Node Exporter runs as a containerized application in Kubernetes to collect metrics from each node.
PART 1 — Install Kubernetes (Minikube) on Ubuntu
Minikube is the easiest option for a lightweight Kubernetes cluster inside a VM.

STEP 1 — Install Required Dependencies
Run inside Ubuntu terminal:

sudo apt update

SudoUpdate

sudo apt install -y curl wget apt-transport-https ca-certificates conntrack

Conntrack

STEP 2 — Install Docker (Container Runtime)
sudo apt install -y docker.io

InstallDocker

sudo systemctl enable docker

enableDocker

sudo systemctl start docker

StarsDocker

sudo usermod -aG docker $USER

eanbleduser

Log out and back in so Docker permissions take effect.

STEP 3 — Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

InstallMinikube

sudo install minikube-linux-amd64 /usr/local/bin/minikube

InstallMiniKube

STEP 4 — Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

InstallKubectl

sudo install kubectl /usr/local/bin/

kubectl

STEP 5 — Start Minikube on Desktop
minikube start --driver=docker --cpus=4 --memory=4096

StartMiniKube

Verify:

kubectl get nodes

KubectlGetNode

You should see: minikube Ready

PART 2 — Install Prometheus on Kubernetes
We’ll install basic Prometheus using a Deployment + Service (not Helm), since our task assumes a simple configuration.

STEP 1 — Create monitoring namespace
kubectl create namespace monitoring

NameSpaceMonitoring

STEP 2 — Deploy Prometheus YAML
Create file:

Create a YAML file for the Node Exporter DaemonSet:
vim prometheus-deploy.yaml

Paste: Prometheusyml Prometheusyml Prometheusyml

Apply the YAML file using kubectl:
kubectl apply -f prometheus-deploy.yaml

PromethuesDeploy

Verify the deployment:
kubectl get pods -n monitoring

PrometheusRunning

PART 3 — Deploy Node Exporter as DaemonSet
Create:

vim node-exporter-daemonset.yaml

NodeExporter

Paste your YAML:

ExporterYMLFile

YAMLFileIncluded

RemainingYAMLFile

Apply:

kubectl apply -f node-exporter-daemonset.yaml

DaemonsetCreated

Verify:

kubectl get daemonset -n monitoring

VerifyDaemonset

Create Node Exporter Service
vim node-exporter-service.yaml

NodeService

NodeServiceCode

NodeServiceCreated

Apply it:

kubectl apply -f node-exporter-service.yaml

NodeServiceApply

Prometheus will now detect node-exporter automatically (because of the scrape job added earlier).

PART 4 — Access Prometheus UI
Access the Prometheus UI (e.g., by port-forwarding):

kubectl port-forward svc/prometheus 9090:9090 -n monitoring

portforwarding

Go to:

http://localhost:9090

Webpage

PART 5 — Explore Metrics Provided by Node Exporter
In the Prometheus UI query bar, test:

CPU Metrics

node_cpu_seconds_total

Memory

node_memory_MemAvailable_bytes

Disk

node_filesystem_avail_bytes

Network

rate(node_network_receive_bytes_total[5m])

Conclusion
By completing this project, we’ve set up Prometheus Node Exporter on Kubernetes, enabling comprehensive monitoring of node-level metrics. we’ve also integrated Node Exporter with Prometheus, learned to query metrics, and explored the data it provides. This setup can now be extended with dashboards (e.g., Grafana) or alerts for advanced monitoring needs.