# Continuous Delivery

### Setup Github Repository
1. Locate the https://github.com/pivotal-education/pcf-articulate-code on GitHub
2. Use the Fork button to make your own private copy of the project in your own GitHub account.

### Install Jenkins

Install Jenkins on your local machine or use AWS Jenkins AMI.

#### Local Installation

1. Prior to installing Jenkins the following should have been installed. If not, you will need to do so now.
   - [JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
   - [git](https://git-scm.com/)
   
2. Use [this link](http://mirrors.jenkins-ci.org/war-stable/1.642.4/jenkins.war) to download Jenkins version 1.642.4 war file.
3. Copy the file to folder: pivotal-cloud-foundry-developer-workshop/jenkins/
4. Change the working directory to where you copied the jenkins.war file.
5. Run Jenkins.

    ```java -jar jenkins.war```

6. Open a browser to [http://localhot:8080](http://localhot:8080)

#### AWS Jenkins AMI (Optional)

Provision a [Jenkins instance on AWS](https://aws.amazon.com/getting-started/projects/setup-jenkins-build-server/).

#### Configure Jenkins

You may skip this section if using the AWS Jenkins AMI.

1. Click on the Manage Jenkins link, then click the Manage Plugins link.
2. Click on the Available tab, and find the GitHub plugin. (You can search using the Filter box in the top
right corner.) Select it and click Install without restart.
3. Also install the Cloud Foundry Plugin. Select it and click Install without restart.
4. From the Manage Jenkins page, click on Configure System. Scroll down to the Maven section, and click
the Add Maven button.
5. Enter a name into the name field then, at the bottom of the page, click Save.

#### Create Build Job

1. From the Jenkins dashboard, click New Item (in top left corner), name it articulate-{{your initials}} and
select Maven project Then click OK.
2. Under Source Code Management, select Git, and supply your forked repository URL.
3. Under Build Triggers, select Poll SCM. In the Schedule, enter the CRON formatted string such as * * *
* *. This will poll your Github repository every minute for changes, and if any are detected, will execute
the build.
4. Under Build, add the project path to the Root POM, so it becomes pom.xml.
5. Under Post-build Actions, click the Add post-build action, and select Push to Cloud Foundry.
6. Fill in the parameters to target and log into the Cloud Foundry instance you’ll be using. You will have to
add your credentials. Test the connection to make sure you can connect. Also check the Reset app if
already exists checkbox. This allows for app bits and configuration to be updated/reset with each
deployment; creating a more dependable way to redeploy the application (see the context sensitive help in
Jenkins for more details).
7. Make sure that Enter configuration in Jenkins is selected.

Fill in the following fields:

  - Application Name = articulate-{{initials}}
  - Memory = 768M
  - Hostname = come up with something original and unique
  - Instance = 1
  - Timeout = 60
  - Services = attendee-service

Advanced Settings:
  - Application Path = target/articulate-0.0.1-SNAPSHOT.jar

8. Save the config and try running the build by clicking Build Now. Do not proceed past this step until you
have a successful build and deployment to Pivotal Cloud Foundry. Confirm the application is deployed by
viewing it in your browser.

Make sure to view the Build details (Left side of screen -> Build History -> Build #).
Console Output can be viewed there (for active or completed jobs). This is very useful for debugging
failing builds.

9. In your forked repo, edit the Welcome message for Articulate.

   a. Edit the following file (can be done with a browser):

   https://github.com/{{github_username}}/pcf-articulate-code/blob/master/src/main/resources/templates/index.html

   b. Change the welcome message from ```Welcome to Articulate!``` to ```Welcome to My Articulate
   Application!```. Commit and push the change to GitHub, wait until the polling detects it, and watch the
   magic. Verify the build in Jenkins now succeeds. Also verify your change in the deployed application
   with a browser.
