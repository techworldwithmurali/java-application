+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline Job - Dockerizing and Pushing to AWS ECR.</br>

## Jenkins Pipeline Job - Dockerizing and Pushing to AWS ECR..

### Prerequisites:
+ Jenkins is installed
+ Docker is installed
+ AWS cli is installed
+ IAM user is created.  User name: dev
+ Github token generate

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration
 + Pipeline: AWS Steps

### Step 2: Create the AWS ECR repository
```xml
Name: web-application
```

### Step 3: Create the Jenkins Pipeline job
```xml
Job Name: pushing-docker-image-to-ecr
```
### Step 4: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : pushing-docker-image-to-ecr-jenkinsfile
```
### Step 5: Write the Dockerfile
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
                git branch: 'pushing-docker-image-to-ecr-jenkinsfile', url: 'https://github.com/techworldwithmurali/java-application.git'
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
              docker tag web-application:latest 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:latest
                
                '''
                
            }
        }
   
```
+ ### 6.4: Push Docker Image to AWS ECR

```xml
stage('Push Docker Image') {
 withAWS(credentials: 'AWS', region: 'us-east-1') {
       
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 108290765801.dkr.ecr.us-east-1.amazonaws.com
                   docker push 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:latest
                    '''
                }
            } 
            
        }
```


### Step 7: Verify whether docker image is pushed or not in AWS ECR

#### Congratulations. You have successfully Pushed the docker image to AWS ECR using Jenkins Pipeline job.
