The most common scenarios for the Azure Functions Runtime is unreachable, is the connectivity between the functions host and the storage account set for AzureWebJobsStorage and/or WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

After deploying the ARM template, simply set the storage account networking settings to Enabled from selected virtual networks and IP addresses.

Resolution, either set the storage account to public network access or configure the function app on a VNET/Subnet which is then added to the Firewalls/Virtual Networks setting to allow traffic from the VNET/Subnet. 
Alternatively, you could also review the VNET2StorageAccountPE for setting up Private Endpoints on the Storage account. 
