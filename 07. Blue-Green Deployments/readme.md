# Blue-Green Deployments

1. Scale the ```articulate``` app to 2 instances

    ```cf scale articulate -i 2
    
2. Browse the ```articulate Blue-Green``` page
3. Press the **Start** button to generate traffic to the app
4. Leave the traffic generation running and observe the app handling all the web requests.
5. Make a note of the ```host``` for the ```articulate``` application by running the following command. This is our current Production route. We'll use this in the next step.

    ```cf routes```
    
6. Push the next version of ```articulate```and give it a ```temp``` route by appending ```-temp``` to the production route from previous step.

    ```cd <parent directory>/pcf-lab/articulate/```
    ```cf push articulate-v2 -p ./articulate-0.2.jar -m 768M -n {{articulate_prod_hostname-temp}} --no-start```

7.
