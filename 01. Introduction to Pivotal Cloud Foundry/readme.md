# Introduction to Pivotal Cloud Foundry

## Lab Instructions

By now, you should have logged in to PWS, downloaded and configured CF CLI. If not already logged in via CF CLI, follow the instructions below:

1. Open a command window and enter the following command:

   ``cf login -a api.run.pivotal.io``

2. When prompted, enter your email id and password.
3. Once logged in, we will push some simple applications as below:
4. In the command window cd into the appropriate directory

    ```cd <parent directory>/pcf-developer-training/node```
5. Push the node app using teh command below:

    ```cf push node --random-route -m 128M```
    
6. Once the app has been deployed, enter the following command to view the application details:

    ```cf apps```

7. Copy the application URL and paste it into a browser window.
8. You may also use the curl command as below:

    ```curl <app_url>```

9. You may repeat the steps for the other applications by cd into the appropriate directory and push the app. For example:

    ```cd ../python```
    
    ```cf push python```
    
    ```cf apps```
    
    ```curl <app_url>```
    
10. Go to [PCF Apps Manager](https://console.run.pivotal.io) and review the contents under Org, Space and App
11. Delete the applications

     ```cf delete node```

12. Repeat for other applcations (python, php, ruby) if they were deployed.

