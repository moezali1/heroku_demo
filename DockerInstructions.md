## Deploying Docker Container to Azure Web Apps

Follow the steps below to build your Docker container locally and push it to Azure Web Apps using Azure Container Registry (ACR).

### Step 1: Build the Docker Image Locally

Run the following command inside your project directory (where the Dockerfile is located) to build the Docker image:

```bash
docker build -t <your-image-name> .
```
### Step 2: Log in to Azure
Log in to your Azure account via the Azure CLI:

```bash
az login
```

### Step 3: Log in to Azure Container Registry (ACR)
If you don't have an ACR instance, create one with this command (replace the placeholders with your values):

```bash
az acr create --resource-group <resource-group-name> --name <acr-name> --sku Basic
```
Now, log in to ACR:

```bash
az acr login --name <acr-name>
```

### Step 4: Tag the Docker Image
Tag your Docker image to match the ACR repository format:

```bash
docker tag <your-image-name> <acr-name>.azurecr.io/<your-image-name>:<version-tag>
```

### Step 5: Push the Docker Image to ACR
Push your Docker image to Azure Container Registry:

```bash
docker push <acr-name>.azurecr.io/<your-image-name>:<version-tag>
```

### Step 6: Deploy the Image to Azure Web App
Once the image is in ACR, you can deploy it to an Azure Web App.

Create an Azure Web App (if you don't already have one):

```bash
az webapp create --resource-group <resource-group-name> --plan <app-service-plan-name> --name <webapp-name> --deployment-container-image-name <acr-name>.azurecr.io/<your-image-name>:<version-tag>
```

### Step 7: Verify the Deployment
Verify the deployment by fetching the URL of your web app:

```bash
az webapp show --name <webapp-name> --resource-group <resource-group-name> --query "defaultHostName"
```






