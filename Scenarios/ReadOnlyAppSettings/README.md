When setting READ ONLY app settings in the azure function app, it will cause the Azure Functions Runtime is Unreachable. 

[Read Only App Settings](https://learn.microsoft.com/en-us/azure/app-service/reference-app-settings?tabs=kudu%2Cdotnet#app-environment)

Some of these settings will pass validation, some will fail. Some are not even listed as they are very specific to a scenario. One I will go over in ReadOnlyAppSettings2.

Resolution, is do not use that app setting or set read only app settings. 
