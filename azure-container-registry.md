# AZ Azure Container Registry CLI Command Line Cheat-Sheet

Quick reference for common AZ ACR CLI Commands

## ACR

### Authenticate to Azure Container Registry
```
// Docker Desktop must be running
az acr login -n <registry name>
```

### Build Image and Push to Azure Container Registry (using ACR Tasks)
```
az acr build --registry <container_registry_name> --image <name the image>:<provide tag> .

// Docker file in different sub-directory
az acr build --image <image name>:<tag> --registry <registry name> .

// Pushing from Visual Studio with VS-generated Dockerfile
// start at folder immediately above the referenced folders in the Docker file
// Note usage for file argument where Dockerfile in different directory than from where command launched
az acr build --image catalog-service:v1 --registry <acr name> --file Services/Catalog.Service/dockerfile .
```

### Push to Azure Container Registry (using Docker Desktop)
```
// Push existing image into Azure Container Registry using Docker Desktop

docker tag <target-image:tag> <registry host>/<username>/<image-name>:<tag>

docker tag my-image:v1.0 myacr.azurecr.io/my-image:v1.0

docker push myacr.azurecr.io/my-image:v1.0
```

### Import Image from One Subscription to Another
```
az acr login -n <destination ACR>

az acr import \
  --name <destinationRegistry> \
  --source <sourceRegistry>.azurecr.io/<Image:Tag> \
  --username <SourceRegistryUsername> \
  --password <SourceRegistryPassword>
```
