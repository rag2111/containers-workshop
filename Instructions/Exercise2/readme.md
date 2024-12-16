# Pushing a Dockerized App to Azure Container Registry

Follow these steps to push your Dockerized application to an Azure Container Registry (ACR):

## Prerequisites

1. **Azure CLI**: Ensure you have the Azure CLI installed. You can download it [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
2. **Docker**: Make sure Docker is installed and running on your machine. Download it [here](https://www.docker.com/products/docker-desktop).

## Steps

1. **Log in to Azure:**
    ```sh
    az login
    ```

2. **Set the Azure subscription (if you have multiple subscriptions):**
    ```sh
    az account set --subscription <your-subscription-id>
    ```

3. **Create a resource group:**
    ```sh
    az group create --name <your-resource-group-name> --location <your-location>
    ```

4. **Create an Azure Container Registry with admin access:**
    ```sh
    az acr create --resource-group <your-resource-group-name> --name <your-acr-name> --sku Basic --admin-enabled true
    ```

5. **Log in to your Azure Container Registry:**
    ```sh
    az acr login --name <your-acr-name>
    ```

6. **Build your Docker image:**
    Navigate to the directory containing your Dockerfile and run:
    ```sh
    docker build -t <your-acr-name>.azurecr.io/<your-image-name>:<tag> .
    ```

7. **Push the Docker image to ACR:**
    ```sh
    docker push <your-acr-name>.azurecr.io/<your-image-name>:<tag>
    ```

8. **Verify the image in ACR:**
    ```sh
    az acr repository list --name <your-acr-name> --output table
    ```
Your Dockerized application is now pushed to your Azure Container Registry.
