# Activate Azure Monitoring and Application Insights

To activate Azure Monitoring and Application Insights for your application, follow these steps:

## Prerequisites

1. **Azure CLI**: Ensure you have the Azure CLI installed. You can download it [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
2. **Git CLI**: Ensure you have the Git CLI installed. You can download it [here](https://git-scm.com/).

## Steps

### 1. Authenticate with Azure

Log in to your Azure account using the Azure CLI:

```sh
az login
```

### 2. Scale your AKS Cluster to 3 Nodes

Scale your AKS cluster to 3 nodes:

```sh
az aks scale --name <aks-cluster-name> --resource-group <your-resource-group-name> --node-count 3
```

### 3. Clone the Microservices Demo Repository

Clone the "Online Boutique" microservices demo repository:

```sh
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo
```

### 4. Apply the Kubernetes Manifests

Apply the Kubernetes manifests to deploy the microservices demo:

```sh
kubectl apply -f ./release/kubernetes-manifests.yaml
```

Your application should now be accessible via the external IP address of the service.

### 5. Inspect logs and metrics through Azure Portal

In the Azure portal, go to the AKS cluster → Insights.
Navigate to the Nodes, Controllers, and Containers tabs to observe:
- CPU and memory per node.
- Pod status.
- Individual container metrics.