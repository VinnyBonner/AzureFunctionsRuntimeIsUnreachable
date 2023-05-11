Host ID collision happens when 2 function apps use the same storage account for AzureWebJobStorage and thier names are the same up to 32char. 

![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/f59f93e6-dafa-4315-93bd-5b10ca088b1b)

Resolution is either (explicitly set the hostId)[https://github.com/Azure/azure-functions-host/wiki/Host-IDs#host-id-override] or use a different storage accounts for the AzureWebJobsStorage. 

ARM template to create resources which will cause issue. 

You may need to create a simply Http Trigger via the portal or deploy to one of the apps, to get the other to show Azure Functions Runtime is unreachable. 
