+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually building and pushing artifacts(war) to Jfrog Artifactory</br>

## Manually - Build and Push to Jfrog Artifactory

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ DockerHub Account is created


### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git
 branch name: build-and-push-to-jfrog
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the repository in DockerHub
### Step 4: Write the Dockerfile
### Step 5: Build and tag the Docker image
### Step 6: Login to DockerHub in local
### Step 7: Push the docker image to DockerHub
### Step 8: Verify whether docker image is pushed or not in DockerHub


#### Congratulations. You have successfully Pushed the docker image to DockerHub.
