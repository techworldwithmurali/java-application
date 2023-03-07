+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> https://www.techworldwithmurali.com/ , https://www.devopsbymurali.com/</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Freestyle - Build and Deploy the war file in Tomcat.</br>

## Jenkins Freestyle - Build and Deploy the war file in Tomcat.

### Prerequisites:
  + Jenkins is installed
  + Tomcat 7 is installed
  + Jfrog artifactory is installed
  + Github token generate

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  + artifactory
  
### Step 2: Create the user in Jfrog
```xml
UserName: moole
Password: Techworld@2580
```
### Step 3: Create the maven repository in Jfrog
```xml
Repository Name: web-application
```
### Step 4: Create the Jenkins Freestyle job
```xml
Job Name: build-and-deploy-to-tomcat
```
### Step 5: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : build-and-deploy-to-tomcat-freestyle
```
### Step 6: Configure the Invoke Artifactory Maven 3
      clean install
### Step 7: Configure the Maven3 artifactory Integration

### Step 8: Verify whether artifact(war) is published or not in Jfrog Artifactory.
### Step 9: Configure the tomcat under post build section
### Step 10: Verify whether application is deployed or not properly in tomcat

#### Congratulations. You have successfully deployed the artifact(war) file in Tomcat using Jenkins Freestyle job.
