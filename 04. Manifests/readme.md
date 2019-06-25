# Manifests

## How to reverse-Engineer a manifest from an already running application

1. Change directory to the ```attendee-service``` application

    ```cd <parent directory>/pcf-lab/attendee-service/```
  
2. Generate the manifest file

    ```cf create-app-manifest attendee-service -p ./manifest.yml```
  
3. Make modifications to the manifest file

     - Increase the instances to 2
    - Set the path to the application binary:  ```path: ./attendee-service-0.1.jar```

4. Push ```attendee-service```

    ```cf push```
  
5. Confirm that ```attendee-service``` is running and the parameters specified in manifest are reflected.

    ```cf app attendee-service```
    
6. Decrease the instance back to 1 by modifying the manifest file
7. Push ```attendee-service``` with the new parameter

    ```cf push```
    
## Create a manifest file by hand

1. Change directory to ```articulate``` application

    ```cd <parent directory>/pcf-lab/articulate/```
    
2. Try to create the manifest file from scratch. Refer to the ```attendee-service``` manifest file or use the [Manifest documentation](https://docs.pivotal.io/pivotalcf/2-6/devguide/deploy-apps/manifest.html). Remember, yaml files are indented with two spaces, and should not have any tabs.

3. Once you are satisfied with the manifest file, push the application and see if it properly deploys your
application as before.
