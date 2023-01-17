+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Freestyle - Dockerizing and Pushing to DockerHub.</br>

## Jenkins Freestyle - Dockerizing and Pushing to DockerHub.

### Prerequisites:
+ Jenkins is installed
+  Docker is installed
+  Github token generate

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration

### Step 2: Create the Docker repository
```xml
Name: web-application
```

### Step 3: Create the Jenkins Freestyle job
```xml
Job Name: pushing-docker-image-to-dockerhub
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : pushing-docker-image-to-dockerhub-freestyle
```
### Step 5: Invoke the top level maven targets
```xml
clean package
```
### Step 6: Write the Dockerfile
```xml
FROM tomcat:9
RUN apt update
WORKDIR /usr/local/tomcat
ADD target/*.war webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
### Step 7: Build and tag the Docker image
```xml
docker build . --tag web-application:latest
docker tag web-application:latest mmreddy424/web-application:latest
```
### Step 8: login to DockerHub
```xml
docker login -u mmreddy424 -p Docker@123
```
### Step 9: Push to DockerHub
```xml
docker push mmreddy424/web-application:latest
```
### Step 10: Verify whether docker image is pushed or not in DockerHub

##### Congratulations. You have successfully pushed the docker image to DockerHub using Jenkins freestyle job.
