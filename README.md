+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Freestyle - building and pushing artifacts(war) to Jfrog Artifactory</br>

## Jenkins Freestyle - Build and Push to Jfrog Artifactory

### Prerequisites:
  + Jenkins is installed
  + Github token generate

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  
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
Job Name: build-and-push-to-jfrog
```
### Step 5: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : build-and-push-to-jfrog-freestyle
```
### Step 6: Configure the Invoke Artifactory Maven 3
      clean install
### Step 7: Configure the Maven3 artifactory Integration

### Step 8: Verify whether artifact(war) is published or not in Jfrog Artifactory.

#### Congratulations. You have successfully published the artifact(war) file in Jfrog repository using Jenkins Freestyle job.
