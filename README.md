+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually Deploy to EKS fetching image from DockerHub.</br>

## Manually - Deploy to EKS fetching image from DockerHub.

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ DockerHub repository is created
+ AWS EKS is created

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the repository in DockerHub
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
docker build . --tag web-application:latest
docker tag web-application:latest mmreddy424/web-application:latest
```
### Step 6: Login to DockerHub in local
```xml
docker login
```
### Step 7: Push the docker image to DockerHub
```xml
docker push mmreddy424/web-application:latest
```
### Step 8: Verify whether docker image is pushed or not in DockerHub
### Step 9 : Write the Kubernetes Deployment and Service manifest files.
```xml

apiVersion: apps/v1app
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
---
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
### Step 10: Update the Dockerhub image in deployment.yaml
### Step 11: Connect to the AWS EKS Cluster
### Step 12: Apply the Kubernetes manifest files
### Step 13: Create the secret file for Dockerhub
```xml
kubectl create secret docker-registry regcred --docker-server=https://hub.docker.com/ --docker-username=mmreddy424 --docker-password=Docker@123 --docker-email=techworldwithmurali@gmail.com

  imagePullSecrets:
  - name: regcred

```
### Step 13: Access nodejs application through NodePort.


#### Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS).
