Just like the VNET2StorageAccountFW, the common cause of the Azure Functions Runtime is unreachable is network connectivity between the functions host and the storage account set in AzureWebJobsStorage and/or WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

In this scenario the storage account has private endpoints on the Blob (used by AzureWebJobStorage) and File (WEBSITE_CONTENTAZURECONNECTIONSTRING) and the function host is unable to connect to the storage account. 
