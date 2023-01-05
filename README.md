+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually Deploy to EKS using Helmchart through DockerHub.</br>

## Manually - Deploy to EKS using Helmchart through DockerHub

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ DockerHub Account is created
+ AWS EKS is created
+ Helm3 is installed

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git
 branch name: deploy-to-eks-helmchart-dockerhub
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
### Step 9 : Create the helm chart and update the helm chart files.
### Step 10: Connect to the AWS EKS Cluster
### Step 11: Install the helm chart using helm command.
### Step 12: Access Java application through NodePort.


#### You have successfully Deployed the Java application in Kubernetes(AWS EKS) through Helm Chart.
