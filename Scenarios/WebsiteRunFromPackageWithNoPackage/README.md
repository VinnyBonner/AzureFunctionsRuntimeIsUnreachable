Website run from package with no package will result in a file in the wwwroot showing "FAILED TO INITIALIZE RUN FROM PACKAGE.txt" which will cause the host to shutdown. 

The solution is to either remove the app settings WEBSITE_RUN_FROM_PACKAGE or simply deploy code to the app. 

ARM Template for creating resources with the app setting set to recreate the issue. 
