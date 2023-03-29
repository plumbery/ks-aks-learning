

# Create AKS Clusters

## Step-01: Introduction
- Understand about AKS Cluster
- Discuss about Kubernetes Architecture from AKS Cluster perspective

## Step-02: Create AKS Cluster
- Create Kubernetes Cluster
- **Basics**
  - **Subscription:** vs Enterprise
  - **Resource Group:** Create New: aks-rg1-yourname
  - **Cluster preset configuration:** Standard ($$)
  - **Kubernetes Cluster Name:** aksdemoks1
  - **Region:** (US) Central US
  - **Availibilty zones** Uncheck zones make it none
  - **AKS pricing tier** Free
  - **Kubernetes Version:** Select what ever is latest stable version
  - **Automatix upgrade:** Left it default   
- **Primary node pool**
  - **Node Size:** Standard DS2 v2 (Default one)
  - **Scale Method:** Manual
  - **Node Count:** 1
- **Node Pools**
  - leave to defaults
- **Access**
  - leave to defaults
- **Networking**
  - **Network Configuration:** Azure CNI
  - **Network Policy:** Azure
  - Rest all leave to defaults
- **Integrations**
  - Azure Container Registry: None
  - **Azure Monitor**
    Conatiner Monitoring: Disabled
  - Rest all leave to defaults
- **Advanced**
  - Rest all leave to defaults
- **Tags**
  - leave to defaults
- **Review + Create**
  - Click on **Create**


## Step-03: Cloud Shell - Configure kubectl to connect to AKS Cluster
- Go to https://shell.azure.com
```
# Template
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>

# Replace Resource Group & Cluster Name
az aks get-credentials --resource-group aks-rg1-alper --name aksdemoks1

# List Kubernetes Worker Nodes
kubectl get nodes 
kubectl get nodes -o wide
```

## Step-04: Explore Cluster Control Plane and Workload inside that
```
# List Namespaces
kubectl get namespaces
kubectl get ns

# List Pods from all namespaces
kubectl get pods --all-namespaces

# List all k8s objects from Cluster Control plane
kubectl get all --all-namespaces
```

## Step-05: Explore the AKS cluster on Azure Management Console
- Explore the following features on high-level
- **Overview**
  - Activity Log
  - Access Control (IAM)
  - Security
  - Diagnose and solver problems
- **Settings**
  - Node Pools
  - Upgrade
  - Scale
  - Networking
  - DevSpaces
  - Deployment Center
  - Policies
- **Monitoring**
  - Insights
  - Alerts
  - Metrics
  - and many more 
- **VM Scale Sets**
  - Verify Azure VM Instances
  - Verify if **Enhanced Networking is enabled or not**  



## Step-06: Local Desktop - Install Azure CLI and Azure AKS CLI
```
# Install Azure CLI TO WSL
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
run <az> in ternminal you shold see az respond to command.
close to terminal and open new one for activate auto complate.
# Login to Azure
az login --use-device-code

# Install Azure CLI (MAC)
brew update && brew install azure-cli



# Install Azure AKS CLI
az aks install-cli

# Configure Cluster Creds (kube config)
az aks get-credentials --resource-group aks-rg1 --name aksdemoks1

# List AKS Nodes
kubectl get nodes 
kubectl get nodes -o wide
```
- **Reference Documentation Links**
- https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest
- https://docs.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest

## Step-07: Deploy Sample Application and Test
- Don't worry about what is present in these two files for now. 
- For now just focus on result. 
```
# Deploy Application
kubectl apply -f kube-manifests/

# Verify Pods
kubectl get pods

# Verify Deployment
kubectl get deployment

# Verify Service (Make a note of external ip)
kubectl get service

# Access Application
http://<External-IP-from-get-service-output>
```

## Step-07: Clean-Up
```
# Delete Applications
kubectl delete -f kube-manifests/
```

## References
- https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest

## Why Managed Identity when creating Cluster?
- https://docs.microsoft.com/en-us/azure/aks/use-managed-identity
