# Services

In this lab, we will create and use both managed services and user-provided services. To facilitate this, we will deploy the ```attendee-service``` application.

### Push the ```attendee-service``` app
1. Open a command window and cd into the ```attendee-service``` dorectory

    ```cd <parent directory>/pcf-developer-training/attendee-service```
2. Push the ```attendee-service``` application

    ```cf push attendee-service -p ./attendee-service-0.1.jar -m 768M --random-route```

You will notice that the ```cf push``` produced some errors and ```attendee-service``` app did not start correctly. It is because the app depends on a database which is not provisioned or linked. Let's go ahead and provision a MySQL instance from PWS Marketplace and bind ```attendee-service``` to it.

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
