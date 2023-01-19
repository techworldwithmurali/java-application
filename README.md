+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins freestyle - Dockerizing and Pushing to Jfrog repository.</br>

## Jenkins freestyle - Dockerizing and Pushing to Jfrog repository.

### Prerequisites:
  + Jenkins is installed
  + Docker is installed
  + Github token generate

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  
### Step 2: Create the user in Jfrog
```xml
UserName: moole
Password: Techworld@2580
```
### Step 3: Create the docker repository in Jfrog
```xml
Repository Name: web-application
```
### Step 4: Create the Jenkins Freestyle job
```xml
Job Name: pushing-docker-image-to-jfrog
```

### Step 5: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : pushing-docker-image-to-jfrog-freestyle
```

### Step 6: Invoke the top level maven targets
```xml
clean package
```
### Step 7: Write the Dockerfile
```xml
FROM tomcat:9
RUN apt update
WORKDIR /usr/local/tomcat
ADD target/*.war webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
### Step 8: Build the Docker image
```xml
docker build . --tag web-app:$BUILD_NUMBER
```
### Step 9: Login to Jfrog in local
```xml
docker login -u moole -p Techworld@2580 a0twcdxxwofaz.jfrog.io
```
### Step 10: tag and push to Jfrog artifactory
```xml
docker tag web-app:$BUILD_NUMBER a0twcdxxwofaz.jfrog.io/web-application/web-app:$BUILD_NUMBER

docker push a0twcdxxwofaz.jfrog.io/web-application/web-app:$BUILD_NUMBER
```
### Step 11: Verify whether docker image is pushed or not in Jfrog Artifactory

#### Congratulations. You have successfully pushed the docker image to Jfrog Artifactory through Jenkins Freestyle job.
