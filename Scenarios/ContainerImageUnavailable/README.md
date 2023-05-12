Another reason for the Azure Functions Runtime is unreachable error message, is due to issues with pulling an Image from Docker, Azure Container Registry or other Image registries. 

After deploying the ARM template, we will run the below commands to create a local docker image and upload it to an ACR. We will then step through setting up CI/CD to use that Image, and finally restrict network access to cause the error.
Note: Pre-req and additional instructions can be found  [Create a function on Linux using a custom container](https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-function-linux-custom-image?pivots=programming-language-python&tabs=in-process%2Cbash%2Cazure-cli%2Cv1) and [Tutorial: Deploy and use Azure Container Registry (ACR)](https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr?tabs=azure-cli)

In Visual Studio Code -> File -> Open Folder -> Create a new folder and open it -> Terminal -> New Terminal

Run the below commands - NOTE: You will need to replace the content between < > with the correct input

Creates the Python Virtual Env and activates it
```
py -m venv .venv
.venv\scripts\activate
```

Create a new function app for docker, adds a Http Trigger with anonymous auth level and builds the docker image.
```
func init --worker-runtime python --docker
func new --name HttpExample --template "HTTP trigger" --authlevel anonymous
docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .
```

Logs into Azure CLI, creates a resource group and ACR with Premium SKU for networking support, then lists the login server address, which is needed in next steps.
```
az login
az group create --name <myResourceGroup> --location eastus
az acr create --resource-group myResourceGroup --name <acrName> --sku Premium
az acr login --name <acrName>
az acr list --resource-group <myResourceGroup> --query "[].{acrLoginServer:loginServer}" --output table
```
We then need to Tag the image for the ACR server and pushes it to the ACR. 

```
docker tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 <acrLoginServerAddress>/azurefunctionsimage:v1.0.0
docker push <acrLoginServerAddress>/azurefunctionsimage:v1.0.0
```

With the Image pushed to the ACR, we will now configure the CICD.
Azure Portal -> Function App -> Deployment Center and update change the fields and click save.

![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/8bdc86a1-a357-447d-8ea0-e1c8572ae59c)

Now you will notice after a minute that when you go to Functions, you will see the Http Trigger, and under the Deployment Center -> Logs, you can view the Docker logs. 

To force the Azure Functions Runtime is unreachable, you can do the following:
Azure Portal -> Container Registry (ACR) -> Networking, and select Disabled and uncheck "Allow trusted Microsoft services to access this container registry" and click save.

We then need to force the Azure Function App to restart and attempt to pull the image. The easiest way is to Scale up or down. 
Back on the Function App -> Scale Up -> Select a plan to scale up or down and wait about 2 minutes.

Now switch to the Overview blade and click on the URL to see the error:
![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/4978610c-e79f-4a85-b54f-b170922f2999)

On the Functions Blade, you will see "Azure Functions runtime is unreachable"
![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/92d7b42d-df1b-4acb-b3f2-ae30b05e1c16)

And if you view the docker logs, on the Deployment Center -> Logs, you will see something like the below:
![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/3875f82c-068c-4e13-ad88-5c36378b4fcc)




