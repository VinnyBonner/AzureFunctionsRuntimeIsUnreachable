Website run from package with no package will result in a file in the wwwroot showing "FAILED TO INITIALIZE RUN FROM PACKAGE.txt" which will cause the host to shutdown. 

![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/1b9ccbbd-b9ee-4f02-9987-0c5512b6d6e5)

The solution is to either remove the app settings WEBSITE_RUN_FROM_PACKAGE or simply deploy code to the app. 

ARM Template for creating resources with the app setting set to recreate the issue. 

Diagnose and solve problems blade -> Function app down or reporting errors -> Functions that are not triggering:
![image](https://github.com/VinnyBonner/AzureFunctionsRuntimeIsUnreachable/assets/92878154/137500bf-4faa-4b1d-a217-2100b7bf1546)
