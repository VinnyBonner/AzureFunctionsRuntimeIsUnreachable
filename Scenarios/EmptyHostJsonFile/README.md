When a Function App gets in a state where the host.json file is empty, like caused be from a deployment which has a empty host.json file. 

![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/4c1bca11-d1ad-494d-abc5-1fe6978bad36)

The resolution is to update the host.json file with valid host content. 

Simple example from a starter function is:

```
{
    "version": "2.0",
    "logging": {
        "applicationInsights": {
            "samplingSettings": {
                "isEnabled": true,
                "excludedTypes": "Request"
            }
        }
    }
}
```
