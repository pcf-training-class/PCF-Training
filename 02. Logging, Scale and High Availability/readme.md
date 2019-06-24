# Logging, Scale and High Availability
## Lab Instructions

Now that we pushed some simple apps, let's go one step further. Let's push a bigger app and view/tail logs, view the application events and scale the application. Follow the instructions below:

### Tail Logs
1. Open a command window and cd into the ```articulate``` directory

    ```cd <parent directory>/pcf-lab/articulate```

2. Push the ```articulate``` application

     ```cf push articulate -p ./articulate-0.2.jar -m 768M --random-route --no-start```

3. Review and understand the parameters used
4. Tail the logs for the ```articulate``` application

    ```cf logs articulate```

5. ```cf logs``` utilizes Websocket connection. If your company's firewall blocks Websocket connections, then you will not be able to see the logs. In that case, use the Apps Manager to view the logs.
6. Open another terminal window and start the ```articulate``` application.

    ```cf start articulate```
7. View the ```articulate``` application in a browser. Refresh the screen a few times. Watch the logs.
8. Stop tailing logs by issuing Ctrl+C or pausing the logs in Apps Manager

### View Events
9. View the events assocated with ```articulate``` application

    ```cf events articulate```
    
    You can view the events in Overview tab of the Apps Manager as well.

### Scale the app
10. Now let's scale the application both vertically (scale up) and horizontally (scale out).
11. Start tailing the logs again with additional parameters

####    Mac, Linux, Powershell

   ```cf logs articulate | grep "API\|CELL"```
    
####    Windows

    ```cf logs articulate | findstr API CELL```

 
