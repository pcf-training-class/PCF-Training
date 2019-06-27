# Application Security Groups

### Review Application Security Groups

1. View the security groups in your environment

    ```cf security-groups```
  
2. PCF has multiple security groups set up. View a couple of them.

    ```cf security-group public_networks```
  
3. View the differences in what you can see when logged in as admin Vs user

### Staging Security Groups and Running Security Groups

4. View the security groups that are in force when applications are staged and when they are running.

    ```cf staging-security-groups```
    
    ```cf running-security-groups```
