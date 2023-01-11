+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually building and pushing artifacts(war) to Jfrog Artifactory and deploy to tomcat.</br>

## Manually - Build and Push to Jfrog Artifactory and deploy to tomcat.

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Jfrog Artifactory is installed
+ Create maven repository in Jfrog
+ Tomcat 7 is installed

### Step 1: Clone the repository
  ```xml
  git clone https://github.com/techworldwithmurali/java-application.git
```
### Step 2: Create the user in Jfrog
```xml
User Name: moole
```
### Step 3: Create the maven repository in Jfrog
```xml
Repository Name: web-application
```
### Step 4: Update the jfrog Artifactory details in pom.xml
```xml
 <distributionManagement>
      <snapshotRepository>
        <id>jfrog-snapshots</id>
        <url>https://devopsbymurali.jfrog.io/artifactory/web-application/</url>
      </snapshotRepository>
      <repository>
        <id>jfrog-releases</id>
        <url>https://devopsbymurali.jfrog.io/artifactory/web-application/</url>
      </repository>
    </distributionManagement>
```

### Step 5: Update the jfrog credentials in settings.xml
```xml
<servers>
    <server>
      <id>jfrog-snapshots</id>
      <username>moole</username>
      <password>moole2580</password>
    </server>
    <server>
      <id>jfrog-releases</id>
      <username>moole</username>
      <password>moole2580</password>
    </server>
  </servers>
```
### Step 6: Run the below command to push the artifacts to Jfrog Artifactory.
```sh
mvn deploy
```
### Step 7: Verify whether artifact(war) is published or not in Jfrog Artifactory.

### Step 8 : Deploy the war file in Tomcat webapps folder.
### Step 10 : Verify whether application is up and running or not

#### Congratulations. You have successfully deployed the artifact(war) file in Tomcat.
