When setting READ ONLY app settings in the azure function app, it will cause the Azure Functions Runtime is Unreachable. 

[Read Only App Settings](https://learn.microsoft.com/en-us/azure/app-service/reference-app-settings?tabs=kudu%2Cdotnet#app-environment)

Some of these settings will pass validation, some will fail. Some are not even listed as they are very specific to a scenario. One I will go over in ReadOnlyAppSettings2.

Resolution, is do not use that app setting or set read only app settings. 

```
Environment Variables I have tested if it would pass validation:
WEBSITE_SITE_NAME - Fails
WEBSITE_RESOURCE_GROUP - Succeeds
WEBSITE_OWNER_NAME - Succeeds
REGION_NAME - Succeeds
WEBSITE_PLATFORM_VERSION - Succeeds
HOME - Fails
SERVER_PORT - Succeeds
WEBSITE_COMPUTE_MODE - Fails
WEBSITE_SKU - Fails
SITE_BITNESS - Succeeds
WEBSITE_HOSTNAME - Fails
WEBSITE_VOLUME_TYPE - Succeeds
WEBSOCKET_CONCURRENT_REQUEST_LIMIT - Succeeds
WEBSITE_SCM_ALWAYS_ON_ENABLED - Succeeds
WEBSITE_SCM_SEPARATE_STATUS - Succeeds
```
