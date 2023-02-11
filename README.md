+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins pipeline - Deploy to EKS fetching image from Jfrog repository.</br>

## Jenkins pipeline - Deploy to EKS fetching image from Jfrog repository.

### Prerequisites:
+  Jenkins is installed
+  Docker is installed
+  Github token generate
+  AWS CLI is installed
+  AWS EKS Cluster is created
+  AWS IAM User user created
+  kubectl is installed

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  + Pipeline: AWS Steps
  
### Step 2: Create the user in Jfrog
```xml
UserName: moole
Password: Techworld@2580
```
### Step 3: Create the docker repository in Jfrog
```xml
Repository Name: web-application
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
### Step 7: Write the Kubernetes Deployment and Service manifest files.
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
        image: devopsmurali.jfrog.io/web-application/web-app:latest
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
### Step 5: Create a secret yaml file for Jfrog  credenatils using kubectl
```xml
 kubectl create secret docker-registry jfrogcred \
--docker-server=https://devopsmurali.jfrog.io \
--docker-username=moole \
--docker-password=Techworld@2580 \
--dry-run=client -o yaml > secret.yaml
```
###### Output:
```xml
apiVersion: v1
data:
  .dockerconfigjson: eyJhdXRocyI6eyJodHRwczovL2Rldm9wc211cmFsaS5qZnJvZy5pbyI6eyJ1c2VybmFtZSI6Im1vb2xlIiwicGFzc3dvcmQiOiJUZWNod29ybGRAMjU4MCIsImF1dGgiOiJiVzl2YkdVNlZHVmphSGR2Y214a1FESTFPREE9In19fQ==
kind: Secret
metadata:
  name: jfrogcred
type: kubernetes.io/dockerconfigjson
```
```xml
imagePullSecrets:
- name: jfrogcred
```

### Step 4: Create the Jenkins Pipeline job
```xml
Job Name: deploy-to-eks-jfrog-jenkins-pipeline
```

### Step 5: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : deploy-to-eks-jfrog-jenkinsfile
```

### Step 8: Write the Jenkinsfile
  + ### Step 8.1: Clone the repository 
```xml
stage('Clone') {
            steps {
                git branch: 'deploy-to-eks-jfrog-jenkinsfile', url: 'https://github.com/techworldwithmurali/java-application.git'
            }
        }
```
  + ### Step 8.2: Build the code
```xml
stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
```
  + ### Step 8.3: Build Docker Image
```xml
stage('Build Docker Image') {
            steps {
                sh '''
                docker build . --tag web-app:$BUILD_NUMBER
              docker tag web-app:latest devopsmurali.jfrog.io/web-application/web-app:$BUILD_NUMBER
                
                '''
                
            }
        }
   
```
+ ### Step 8.4: Push Docker Image to Jfrog artifactory
```xml
stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'jfrog_crdenatils', passwordVariable: 'JFROG_PASSWORD', usernameVariable: 'JFROG_USERNAME')]) {
       
                    sh '''
                    docker login -u $JFROG_USERNAME -p $JFROG_PASSWORD devopsmurali.jfrog.io
                        docker push devopsmurali.jfrog.io/web-application/web-app:$BUILD_NUMBER
                    '''
                }
            } 
            
        }
```
+ ### Step 8.5: Deploy to AWS EKS
```xml
stage('Deployto AWS EKS') {
            steps {
                // configure AWS credentials
               withAWS(credentials: 'AWS', region: 'us-east-1') {

                    // Connect to the EKS cluster
                    sh '''
                     aws eks update-kubeconfig --name dev-cluster --region us-east-1'

                    // apply YAML files to EKS cluster
                      cd kubernetes-yaml
                      kubectl apply -f .
                      kubectl set image deployment/web-app web-application=devopsmurali.jfrog.io/web-application/web-app:$BUILD_NUMBER
                    '''
                }
           
        }
            
        }
```

### Step 8:Verify whether pods are running or not
```xml
kubectl get pods -A
```
### Step 9: Create a secret file for Jfrog credenatils
```xml
kubectl create secret docker-registry jfrogcred \
--docker-server=https://a0twcdxxwofaz.jfrog.io \
--docker-username=moole \
--docker-password=Techworld@2580
```
```xml
  imagePullSecrets:
  - name: jfrogcred
```
### Step 10: Access java application through NodePort.
```xml
http://Node-IP:port/web-application
```
#### Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS) through Jenkins Pipeline job.
