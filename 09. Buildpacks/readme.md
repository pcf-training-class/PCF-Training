# Buildpacks

### Use a custom buildpack

1. View the ```articulate``` application in the browser. Make a note of the ```Java Version``` under **Application Environment Information**
2. Find out which buildpak is used by ```articulate```

  ```cf app articulate```
  
3. Push the ```articulate``` application again, but this time we'll specify a custom buildpack. In this case, we will use the latest version of the Java Buildpack on GitHub

  ```cd <parent directory>/cf-lab/articulate```
  
  ```cf push articulate -p ./articulate-0.2.jar -b https://github.com/cloudfoundry/java-buildpack.git```
  
4. Go back to the browser and refresh the ```articulate``` application page. Notice that the ```Java Version``` under **Application Environment Information** has changed.

### Change the Java version

1. Let's run ```articulate``` on a specific verison of Java.

  ```cf set-env articulate JBP_CONFIG_OPEN_JDK_JRE "{jre: { version: 1.8.0_45 }}"```
  
2. Go back to the browser and refresh the ```articulate``` application page. Did the Java version change? Why not?
3. Restart the ```articulate``` application

  ```cf restart articulate```
  
4. Go back to the browser and refresh the ```articulate``` application page. Did the Java version change now? Why not?
5. Restage the ```articulate``` application

  ```cf restage articulate```

6. Go back to the browser and refresh the ```articulate``` application page. Did the Java version change now? Why?
