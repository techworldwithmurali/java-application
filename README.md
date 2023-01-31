+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline - Dockerizing and Pushing to DockerHub.</br>

## Jenkins Pipeline - Dockerizing and Pushing to DockerHub.

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

### Step 3: Create the Jenkins Pipeline job
```xml
Job Name: pushing-docker-image-to-dockerhub-jenkins-pipeline
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : pushing-docker-image-to-dockerhub-jenkinsfile
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

### Step 6: Write the Jenkinsfile
  + ### Step 6.1: Clone the repository 
```xml
stage('Clone') {
            steps {
                git branch: 'pushing-docker-image-to-dockerhub-jenkinsfile', url: 'https://github.com/techworldwithmurali/java-application.git'
            }
        }
```
  + ### Step 6.2: Build the code
```xml
stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
```
  + ### 6.3: Build Docker Image
```xml
stage('Build Docker Image') {
            steps {
                sh '''
               docker build . --tag web-application:latest
               docker tag web-application:latest mmreddy424/web-application:latest
                
                '''
                
            }
        }
   
```
+ ### Push Docker Image
```xml
stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_crdenatils', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
       
                    sh '''
                    docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD
                        docker push mmreddy424/web-application:latest
                    '''
                }
            } 
            
        }
```


### Step 10: Verify whether docker image is pushed or not in DockerHub

##### Congratulations. You have successfully pushed the docker image to DockerHub using Jenkins Pipeline job.
