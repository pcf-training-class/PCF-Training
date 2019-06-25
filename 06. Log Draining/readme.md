# Log Draining

1. Signup for a free [Papertrail account](https://papertrailapp.com/)
2. Once the account is created, go to the [setup link for Cloud Foundry](papertrailapp.com/systems/new)
3. Select "I use Cloud Foundry"
4. "What should we call it?" give it a name: **log-drain**
5. Click "Save"
6. Take note of the url (logsN.papertrail.com:<port-number>) and use it in the next step in place of '''{{syslog_drain_url}}```
7. Create a User Provided Service Instance that streams logs to Papertrail.

    ```cf create-user-provided-service articulate-log-drain -l syslog://{{syslog_drain_url}}```
   
8. Bind the ```articulate-log-drain``` service to the ```articulate``` application.

    ```cf bind-service articulate articulate-log-drain```
 
9. View ```articulate``` app in a browser. Refresh the app a few times to generate logs.
10. To view the logs in Papertrail do the following:
    - Click on "Dashboard"
    - Click on "log-drain"
11. Restart the ``articulate``` application and watch all the logs including the **Spring** logo.    
