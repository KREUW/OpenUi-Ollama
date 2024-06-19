# OpenUi-Ollama LowKey 

This repository contains the Docker image for OpenUi-Ollama, a customized container including OpenWeb UI, Ollama, Python. The Git repository is integrated into the backend along with Python 3.2 to allow pulls from the Ollama repo.

## Table of Contents
- Overview
- Features
- Changes from Original
- Installation
- Usage
- Docker Image
- Deploy to Azure

## Overview
OpenUi-Ollama is designed to provide an easy-to-deploy container environment that integrates OpenWeb UI with Ollama capabilities. This setup is ideal for developers looking to streamline their deployment process by combining both tools into a single, cohesive Docker image with the backend git repos pull built in.

## Features
- **Integrated OpenWeb UI**: Provides a web-based interface for interacting with the application.
- **Ollama Repository Integration**: Allows seamless pulls and integration from the Ollama repository.
- **Python 3.2 Support**: Ensures compatibility and allows for advanced scripting and automation tasks.
- **Pre-configured Docker Environment**: Simplifies deployment with all necessary dependencies included.

## Changes from Original
This version of the container includes the following modifications:
- **Integration of OpenWeb UI and Ollama**: Combines functionalities of both tools.
- **Inclusion of Python 3.2**: Supports pulls from the Ollama repository and additional scripting.
- **Pre-configured Docker Environment**: Ready-to-use setup with all dependencies.
- **Port Configuration**: Runs on port 8080 internally and mapped to port 3000 externally for accessibility.

## Installation
Clone the repository to your local machine:
```sh
git clone https://github.com/KREUW/OpenUi-Ollama.git
cd OpenUi-Ollama
```

## Usage
To start using OpenUi-Ollama, follow these steps:

### Build the Docker image:
```sh
Copy code
docker build -t openui-ollama
```
### Run the Docker container:
```sh
docker run -d -p 3000:8080 openui-ollama
```
Access the application at http://localhost:3000.

## Docker Image
The Docker image is hosted on GitHub Container Registry. You can pull and run the image using the following commands:

```sh
docker pull ghcr.io/kreuw/openui-ollama:latest
docker run -d -p 3000:8080 ghcr.io/kreuw/openui-ollama:latest
```
## Deploy to Azure
To deploy the Docker image to Azure, follow these steps:

### Login to Azure:

```sh
az login
```
### Create a Resource Group:

```sh
az group create --name myResourceGroup --location eastus
```
### Create a Container Registry:

```sh
az acr create --resource-group myResourceGroup --name myContainerRegistry --sku Basic
```
### Login to the Container Registry:

```sh
az acr login --name myContainerRegistry
```
### Tag the Docker Image:

```sh
docker tag openui-ollama:latest mycontainerregistry.azurecr.io/openui-ollama:latest
```
### Push the Docker Image to Azure Container Registry:

```sh
docker push mycontainerregistry.azurecr.io/openui-ollama:latest
```
### Create a Container Instance:
```sh
az container create --resource-group myResourceGroup --name openui-ollama-container --image mycontainerregistry.azurecr.io/openui-ollama:latest --cpu 2 --memory 4 --registry-login-server mycontainerregistry.azurecr.io --registry-username <username> --registry-password <password> --ip-address public --ports 8080
```
##Get the assinged Public IP Address:

```sh
az container show --resource-group myResourceGroup --name openui-ollama-container --query ipAddress.ip --output tsv
```
## Access the Application:
Open a web browser and navigate to the **public IP address obtained in the previous step with the assigned port**.

# Memory for the application is volitaile and will require additional storade to maintiain persistance at container restart.
