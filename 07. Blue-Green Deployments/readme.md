# Blue-Green Deployments

1. Before deploying the new version of the app, let's scale the current version of ```articulate``` app to 2 instances

    ```cf scale articulate -i 2```
    
2. Browse the ```articulate Blue-Green``` page
3. Press the **Start** button to generate traffic to the app
4. Leave the traffic generation running and observe the articulate app handling all the web requests.
5. Make a note of the ```host``` for the ```articulate``` application by running the following command. This is our current Production route. We'll use this in the next step.

    ```cf routes```
    
6. Push the next version of ```articulate```and give it a ```temp``` route by appending ```-temp``` to the production route from previous step.

    ```cd <parent directory>/pcf-lab/articulate/```
    
    ```cf push articulate-v2 -p ./articulate-0.2.jar -m 768M -n {{articulate_prod_hostname-temp}} --no-start```

7. Stop the attendee-service app to free up memory in your org.

    ```cf stop attendee-service```
        
8. Start the new version of articulate app.
    
    ```cf start articulate-v2```
    
9. Now there are 2 versions of the articulate app deployed. Open a new browser tab to view this application.
10. When the new version of the app is ready to take production load, we can map the production route to it.

    ```cf map-route articulate-v2 {{domain_name}} --hostname {{articulate_hostname}}```
    
    for example, ```cf map-route articulate-v2 cfapps.io --hostname articulate-acotyledonous-hornlessnes```
 
11. In the browser, go to the tab where the requests are being sent to the app. You should see that it is starting to send requests to version 2 of the app.
12. Press the **Reset** button so that the load distribution starts new and we can observe the pattern. About one third of the traffic should now be going to version 2 and two thirds going to version 1. (this depends on the number of instances running for each version) 
13. We can now move more traffic to version 2 by adjusting the number of instances for both versions.

    ```cf scale articulate -i 1```
    
    ```cf scale articulate-v2 -i 2```

14. If you **Reset** the load generator, you will now see 2/3 of the traffic going to articulate-v2.
15. Now let's move all traffic to version 2 by removing the production route from version 1 of the articulate application

    ```cf unmap-route articulate {{domain_name}} --hostname {{articulate_hostname}}```
    
    for example: ```cf unmap-route articulate cfapps.io --hostname articulate-acotyledonous-hornlessness```
    
16. If you **Reset** the load generator, you will see that all the traffic is now going to articulate-v2.
17. We can now remove the temp route from the articulate-v2 application.

    ```cf unmap-route articulate-v2 {{domain_name}} --hostname {{articulate_hostname}}```
    
    for example: ```cf unmap-route articulate-v2 {{domain_name}} --hostname {{articulate_hostname}}```
    
18. You have now completed the Blue-Green deployment. **Congratulations"

### Cleanup

1. Now that v2 of articulate is running with the production route, let's delete v1

    ```cf delete articulate```
    
2. Rename articulate-v2 to articulate

    ```cf rename articulate-v2 articulate```
    
3. Restart articulate
    
    ```cf restart articulate```
    
4. Scale down the instances to 1

    ```cf scale articulate -i 1```
    



    

