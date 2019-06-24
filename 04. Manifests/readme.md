# Manifests

## How to reverse-Engineer a manifest from an already running application

1. Change directory to the attendee-service application

  ```cd pcf-lab/articulate/```
  
2. Generate the manifest file

  ```cf create-app-manifest attendee-service -p ./manifest.yml```
  
3. Make modifications to the manifest file

  - Increase the instances to 2
  - Setthe path to the application binary

4. Push ```attendee-service```
