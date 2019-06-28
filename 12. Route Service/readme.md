# Route Service

We will test the Route Service with a rate limiter app. The idea is to control the number of requests to an API. If more than 3 requests come in 15 seconds, we will block the request and give a ```HTTP 429 Too many requests" error```

### Push the rate limiter app

1. Download the zipfile from [here](https://www.dropbox.com/s/ak00xcnu9smaqvj/route-service.zip?dl=1) and extract it to ```<parent directory>/pcf-lab/```
2. Change directory to route-service directory

    ```cd route-service```

3. Push ```rate-limiter-app```

    ```cf push rate-limiter-app -p ./target/route-service-1.0.0.BUILD-SNAPSHOT.jar -m 768M --random-route --no-start```
    
4. Create a Redis service instance.

    ```cf create-service rediscloud 30mb redis```
    
5. Bind the service instance.

    ```cf bind-service rate-limiter-app redis```
    
6. Start the application.

    ```cf start rate-limiter-app```
    
### Create a Route Service and Bind it to a Route

1. Create a user provided service. Let’s call it rate-limiter-service.

    ```cf create-user-provided-service rate-limiter-service -r {{ratelimiter_baseurl}}```
    
2. Bind the rate-limiter-service to the attendee-service route.

    ```cf bind-route-service {{domain_name}} rate-limiter-service --hostname {{attendee_service_hostname}}```
    
### Observe the effects of the rate-limiter-app

 1. Open command window and tail the logs of the rate-limiter-app application.
 
    ```cf logs rate-limiter-app```
    
 2. Open a new tab in Chrome Browser and open **Developer Tools**
 3. Keep both the command window and the browser window side by side.
 4. In the command window, watch the rate limiter resetting every 15 seconds
 5. Go the ```attendees``` endpoint of the ```attendee-service``` app. 
 
    For example: ```attendee-service-bannerlike-nonabdication.cfapps.io/attendees```
    
 6. Reload the ```attendee-service``` endpoint 4 times back to back
 7. View the logs generated as you reload the page each time.
 8. Watch the HTTP Error 429 displayed in **Developer Tools** on the 4th try (within 15 seconds)
 9. View the corresponding logs in the command window.
 
 ### Clean up
 
 1. Unbind the route service.
 
    ```cf unbind-route-service {{domain_name}} rate-limiter-service --hostname {{attendee_service_hostname}}```
    
2. Delete rate-limiter-service service instance.

    ```cf delete-service rate-limiter-service```
    
3. Unbind redis service instance from the app.

    ```cf unbind-service rate-limiter-app redis```
    
4. Delete the redis service instance.

    ```cf delete-service redis```
