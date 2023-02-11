+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline Job - Deploy to EKS fetching image from AWS ECR.</br>

## Jenkins Pipeline Job - Deploy to EKS fetching image from AWS ECR.

### Prerequisites:
+ Jenkins is installed
+ Docker is installed
+ AWS cli is installed
+ AWS EKS is created
+ IAM user is created.  User name: dev
+ Github token generate
+ kubectl is installed

### Step 1: Install and configure the jenkins plugins
 + git
 + maven integration
 + Pipeline: AWS Steps

### Step 2: Create the AWS ECR  repository
```xml
Name: web-application
```
### Step 3: Write the Dockerfile
```xml
FROM tomcat:9
RUN apt update
WORKDIR /usr/local/tomcat
ADD target/*.war webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]

```
### Step 4: Write the Kubernetes Deployment and Service manifest files.
##### deployment.yaml
```xml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  labels:
    app: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-application
        image: 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:latest
        ports:
        - containerPort: 8080
```
##### service.yaml
```xml

apiVersion: v1
kind: Service
metadata:
  name: web-app
  labels:
    app: web-app
spec:
  type: NodePort
  ports:  
    - port: 8080
      targetPort: 8080
  selector:
    app: web-app
```

### Step 5: Create the Jenkins Free style job
```xml
Job Name: deploy-to-eks-ecr-jenkinsfile
```
### Step 6: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : deploy-to-eks-ecr-jenkinsfile
```

### Step 7: Write the Jenkinsfile
  + ### Step 7.1: Clone the repository 
```xml
stage('Clone the repository'){
        steps{
          git branch: 'deploy-to-eks-ecr-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
        } 
      }
```
  + ### Step 7.2: Build the code
```xml
stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
```
  + ### Step 7.3: Build Docker Image
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
+ ### Step 7.4: Push Docker Image to AWS ECR

```xml
stage('Push Docker Image') {
 withAWS(credentials: 'aws-dev-credentials', region: 'us-east-1') {
       
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 108290765801.dkr.ecr.us-east-1.amazonaws.com
                   docker push 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:latest
                    '''
                }
            } 
            
        }
```
+ ### Step 7.5:Deploy to AWS EKS
```xml
stage('Deployto AWS EKS') {
            steps {
                // configure AWS credentials
               withAWS(credentials: 'aws-dev-credentials', region: 'us-east-1') {

                    // configure kubectl to access EKS cluster
                    sh 'aws eks update-kubeconfig --name dev-cluster --region us-east-1'

                    // apply YAML files to EKS cluster
                    sh ' kubectl apply -f kubernetes-yaml/deployment.yaml '
                    sh 'kubectl apply -f kubernetes-yaml/service.yaml'
                    sh 'kubectl set image deployment/web-app web-application=108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:latest'
                }
           
        }
            
        }
```
### Step 8:Verify whether pods are running or not
```xml
kubectl get pods -A
```
### Step 9: Access java application through NodePort.
```xml
http://Node-IP:port/web-application
```
Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS) through Jenkins Pipeline job.
