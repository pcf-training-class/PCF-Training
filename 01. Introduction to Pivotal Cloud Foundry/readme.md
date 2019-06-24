# Introduction to Pivotal Cloud Foundry

## Lab Instructions

By now, you should have logged in to PWS, downloaded and configured CF CLI. If not already logged in via CF CLI, follow the instructions below:

1. Open a command window and enter the following command:

   ``cf login -a api.run.pivotal.io``

2. When prompted, enter your email id and password.
3. Once logged in, we will get comfortable with the CF CLI and then push some simple applications.

### Test drive CF CLI

4. Review the online help on CF CLI

   ``cf help`` or ``cf h`` shows a condensed help of CF CLI commands
   
   ``cf help -a`` or ``cf h -a`` shows all available CF CLI commands in a categorized format.
   
5. Understand Org and Space details.

   ``cf org``
   
   ``cf org <org-name>``
   
   ``cf spaces``
   
   ``cf <space-name>``

### push some simple apps.

6. In the command window, cd into the appropriate directory

    ```cd <parent directory>/pcf-lab/demo-apps/node```
7. Push the node app using the command below:

    ```cf push node --random-route -m 128M```
    
8. Once the app has been deployed, enter the following command to view the application details:

    ```cf apps```

9. Copy the application URL and paste it into a browser window.
10. You may also use the curl command as below:

    ```curl <app_url>```

11. View the application details.

      ``cf app node``

12. You may repeat the steps for other applications by cd into the appropriate directory and push the app. For example:

    ```cd ../python```
    
    ```cf push python```
    
    ```cf apps```
    
    ```curl <app_url>```
    
13. Go to [PCF Apps Manager](https://console.run.pivotal.io) and review the contents under Org, Space and App
14. Delete the applications

     ```cf delete node```

15. Repeat the delete command for other applcations (python, php, ruby) if they were deployed. You may delete the apps from PCF Apps Manager also.

