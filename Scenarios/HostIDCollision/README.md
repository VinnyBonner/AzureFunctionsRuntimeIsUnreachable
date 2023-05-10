Host ID collision happens when 2 function apps use the same storage account for AzureWebJobStorage and thier names are the same up to 32char. 

Resolution is either explicitly set the hostId or use a different storage accounts for the AzureWebJobsStorage. 

ARM template to create resources which will cause issue. 
