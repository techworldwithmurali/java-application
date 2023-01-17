+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually Deploy to EKS fetching image from Jfrog repository.</br>

## Manually - Deploy to EKS fetching image from Jfrog repository.

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ Jfrog docker repository is created
+ AWS EKS is created
+ IAM User is created
+ kubectl is installed
+ AWS cli is installed

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git 
```
### Step 2: build the code
```xml
mvn package
```
### Step 3.1: Create the user in Jfrog
```xml
UserName: moole
Password: Techworld@2580
```
### Step 3.2: Create the docker repository in Jfrog
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
### Step 5: Build and tag the Docker image
```xml
docker build . --tag web-app:latest
```
### Step 6: Login to Jfrog in local
```xml
docker login -umoole a0twcdxxwofaz.jfrog.io
```
### Step 7: Push the docker image to Jfrog Artifactory.
```xml
docker tag web-app:latest a0twcdxxwofaz.jfrog.io/web-application/web-app:latest

docker push a0twcdxxwofaz.jfrog.io/web-application/web-app:latest
```
### Step 8: Verify whether docker image is pushed or not in Jfrog Artifactory
### Step 9 : Write the Kubernetes Deployment and Service manifest files.
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
        image: web-app:1
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
### Step 10: Update the Jfrog artifactory docker image in deployment.yaml
### Step 11: Configure  to the AWS CLI using Access key ID & Secret access key
```xml
aws configure
```
### Step 12: Connect to the AWS EKS Cluster
```xml
aws eks update-kubeconfig --name dev-cluster --region us-east-1
````
### Step 13: Apply the Kubernetes manifest files
```
kubectl apply -f .
```
### Step 14: Verify wether pods are running or not
```
kubectl get pods -A
```
### Step 15: Create a secret file for Jfrog credenatils
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
### Step 16: Access Java application through NodePort.
```
http://Node-IP:port/web-application
```


#### Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS).
