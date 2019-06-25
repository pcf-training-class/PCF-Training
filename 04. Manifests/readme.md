# Manifests

## How to reverse-Engineer a manifest from an already running application

1. Change directory to the attendee-service application

  ```cd <parent directory>/pcf-lab/attendee-service/```
  
2. Generate the manifest file

  ```cf create-app-manifest attendee-service -p ./manifest.yml```
  
3. Make modifications to the manifest file

  - Increase the instances to 2
  - Set the path to the application binary

4. Push ```attendee-service```
