Just like the VNET2StorageAccountFW, the common cause of the Azure Functions Runtime is unreachable is network connectivity between the functions host and the storage account set in AzureWebJobsStorage and/or WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

In this scenario the storage account has private endpoints on the Blob (used by AzureWebJobStorage) and File (WEBSITE_CONTENTAZURECONNECTIONSTRING) and the function host is unable to connect to the storage account. 

After deploying the ARM template there are 2 simple ways to produce the Azure Functions Runtime is unreachable, Though there are many more:

1) By Removing the WEBSITE_CONTENTOVERVNET the functions host will not be able to access the fileshare for WEBSITE_CONTENTAZURECONNECTIONSTRING to load the wwwroot. 
The resolution is adding in WEBSITE_CONTENTOVERVNET.

2) By creating a Blob trigger function to the storage account, the host will not be able to start up. While the host will still have access to the Blob storage to obtain the lease lock, and access the fileshare, the blob trigger uses the Queue endpoint. Due to not being able to create/connect to the Queue endpoint, the host will shutdown. Similar scenarios can happen depending on the functions bindings and triggers. 
The resolution is to ensure their are PE for each of the endpoints needed. We recommend File/Blob/Table/Queue. 

Other Scenarios!
There are many other scenarios involving custom DNS, or the Private Zones having the incorrect IP address, though very rare, it does happen. 

