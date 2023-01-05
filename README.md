+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually Dockerizing and Pushing to Jfrog Artifactory.</br>

## Manually - Dockerizing and Pushing to Jfrog Artifactory

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ Jfrog docker repository is created.

### Step 1: Clone the repository
  
```xml
 github url: https://github.com/techworldwithmurali/java-application.git
 branch name: pushing-docker-image-to-jfrog
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the docker repository in Jfrog Artifactory
### Step 4: Write the Dockerfile
### Step 5: Build and tag the Docker image
### Step 6: Login to Jfrog Artifactory in local
### Step 7: Push the docker image to Jfrog Artifactory
### Step 8: Verify whether docker image is pushed or not in Jfrog Artifactory.


#### Congratulations. You have successfully Pushed the docker image to Jfrog Artifactory.
