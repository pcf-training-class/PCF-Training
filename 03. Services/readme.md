# Services

In this lab, we will create and use both managed services and user-provided services. To facilitate this, we will deploy the ```attendee-service``` application.

**Push the** ```attendee-service``` **app**
1. Open a command window and cd into the ```attendee-service``` dorectory

    ```cd <parent directory>/pcf-lab/attendee-service```
    
2. Push the ```attendee-service``` application

    ```cf push attendee-service -p ./attendee-service-0.1.jar -m 768M --random-route```

    You will notice that the ```cf push``` produced some errors and ```attendee-service``` app did not start correctly. 

    It is because the app depends on a database which is not provisioned or linked. 

    Let's go ahead and provision a MySQL instance from PWS Marketplace and bind ```attendee-service``` to it.

### Provision and bind MySQL service

3. Review the services available in the marketplace

    ```cf marketplace```

    You can see that PWS offers ```cleardb``` MySQL as a managed service and ```spark``` is a plan in the free-tier

4. Create the MySQL service instance

    ```cf create-service cleardb spark attendee-mysql```

5. Bind the app to the MySQL service instance

    ```cf bind-service attendee-service attendee-mysql```

6. Restart the application so that the service binding takes effect

    ```cf restart attendee-service```
    
7. Run the ```attendee-service``` application in browser. You should see a JSON response.
8. In the command window, view the environment for ```attendee-service```

    ```cf env attendee-service```
    
    Different languages/frameworks have various ways to read environment variables. ```attendee-service``` takes advantage of a Java Buildpack feature called Auto-Reconfiguration that automatically re-writes bean definitions to connect with services bound to an application.

### Create and bind to a User Provided Service Instance

9. Create a USer Provided Service

    ```cf create-user-provided-service attendee-service -p uri```
    
    You will be presented with an interactive prompt to enter the ```uri```. 
10. Find the URL for the ```attendee-service``` application from the and enter that value with a ```https://``` prefix. 

    ```uri> https://{{attendees_app_uri}}/```
    
11. Bind articulate to the attendee-service user-provided service.  

    ```cf bind-service articulate attendee-service```
    
12. Restart the ```articulate``` application for the changes to take effect.

    ```cf restart articulate```
    
13. Review the app environment.

    ```cf env articulate```

14. Go to the browser window and refresh the **Services** page. You should now see ```attendee-service``` listed under Services.
15. Add a few attendees.
