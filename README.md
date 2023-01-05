+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually Deploy to EKS fetching image from AWS ECR.</br>

## Manually - Deploy to EKS fetching image from AWS ECR.

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Docker is installed
+ AWS ECR repository is created
+ AWS EKS is created

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git
 branch name: deploy-to-eks-ecr
```
### Step 2: build the code
```xml
mvn package
```
### Step 3: Create the repository in AWS ECR
### Step 4: Write the Dockerfile
### Step 5: Build and tag the Docker image.
### Step 6: Login to  AWS ECR in local
### Step 7: Push the docker image to AWS ECR
### Step 8: Verify whether docker image is pushed or not in AWS ECR
### Step 9 : Write the Kubernetes Deployment and Service manifest files.
### Step 10: Update the ECR docker image in deployment.yaml
### Step 11: Connect to the AWS EKS Cluster
### Step 12: Apply the Kubernetes manifest files.
### Step 13: Access nodejs application through NodePort.


#### Congratulations. You have successfully Deployed the java application in Kubernetes(AWS EKS).
