# Publish the App into AKS

To publish your application into Azure Kubernetes Service (AKS), follow these steps:

## Prerequisites

1. **Azure CLI**: Ensure you have the Azure CLI installed. You can download it [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
2. **Kubectl**: Install `kubectl` to interact with your Kubernetes cluster. Instructions can be found [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

## Steps

### 1. Authenticate with Azure

Log in to your Azure account using the Azure CLI:

```sh
az login
```
### 2. Create an AKS Cluster

Create an AKS cluster:

```sh
az aks create --resource-group <your-resource-group-name> --name <aks-cluster-name> --node-count 1 --enable-addons monitoring --generate-ssh-keys
```

### 3. Attach ACR to AKS

Attach the ACR to your AKS cluster:

```sh
az aks update --name <aks-cluster-name> --resource-group <your-resource-group-name> --attach-acr <your-acr-name>
```

### 4. Get AKS Credentials

Get the credentials for your AKS cluster:

```sh
az aks get-credentials --resource-group <your-resource-group-name> --name <aks-cluster-name>
```

### 5. Deploy Your Application

Create a Kubernetes deployment file (e.g., `deployment.yaml`) for your application. Here is an example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: <your-acr-name>.azurecr.io/<your-image-name>:<tag>
        ports:
        - containerPort: 8080
```

Apply the deployment file to your AKS cluster:

```sh
kubectl apply -f deployment.yaml
```

### 6. Expose Your Application

Expose your application using a Kubernetes service. Create a service file (e.g., `service.yaml`):

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  ports:
  - port: 8080
  selector:
    app: myapp
```

Apply the service file:

```sh
kubectl apply -f service.yaml
```

### 7. Verify the Deployment

Check the status of your pods and services:

```sh
kubectl get pods
kubectl get services
```

Your application should now be accessible via the external IP address of the service.
