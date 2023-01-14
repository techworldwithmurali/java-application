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
### Step 3:
Step 3.1: Create the user in Jfrog
```xml
UserName: moole
Password: Techworld@2580
```
Step 3.2: Create the docker repository in Jfrog Artifactory
```xml
Repository Name: web-application
```
### Step 4: Write the Dockerfile
```xml
FROM tomcat:9
RUN apt update
WORKDIR /usr/local/tomcat
ADD target/*.war webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

### Step 5: Build the Docker image
```xml
docker build . --tag web-application:latest
```
### Step 6: Login to Jfrog Artifactory in local
```xml
docker login -umoole devopsbymurali.jfrog.io
```
### Step 7: Push the docker image to Jfrog Artifactory
```xml
docker tag web-application:latest devopsbymurali.jfrog.io/web-application/web-application:latest

docker push devopsbymurali.jfrog.io/web-application/web-application:latest
```

### Step 8: Verify whether docker image is pushed or not in Jfrog Artifactory.


#### Congratulations. You have successfully Pushed the docker image to Jfrog Artifactory.
