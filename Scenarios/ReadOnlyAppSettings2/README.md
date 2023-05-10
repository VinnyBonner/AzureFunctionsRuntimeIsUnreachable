This is an Edge case for Linux Consumption plans, when setting the App Setting "CONTAINER_NAME"
Behavior does not show "The Azure Functions Runtime is Unreachable" But instead fails to load functions in the Functions Blade due to Container name conflict. 
Code is a simple Http Trigger Function for Python. 
Deployed via AZ CLI
```
az functionapp deployment source config-zip -g <ResourceGroupName> -n <AppName> --src <PathToDownloadedPackage>
```
Reproduce the behavior by adding the App Setting "CONTAINER_NAME" to a Linux Consumption Function App and deploy code. (Can be any code, supplied is for easy repro and is just a starter Python HttpTrigger Function)
