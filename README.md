+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually building and pushing artifacts(war) to Jfrog Artifactory and deploy to tomcat.</br>

## Manually - Build and Push to Jfrog Artifactory and deploy to tomcat.

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Jfrog Artifactory is installed
+ Tomcat 7 is installed

### Step 1: Clone the repository
  
```xml
  github url: https://github.com/techworldwithmurali/java-application.git
 branch name: build-and-push-to-jfrog
```
### Step 2: Update the jfrog Artifactory details in pom.xml

```xml
 <distributionManagement>
      <snapshotRepository>
        <id>jfrog-snapshots</id>
        <url>http://your-host:8081/repository/maven-snapshots/</url>
      </snapshotRepository>
      <repository>
        <id>jfrog-releases</id>
        <url>http://your-host:8081/repository/maven-releases/</url>
      </repository>
    </distributionManagement>
```
### Step 3: Update the jfrog credentials in settings.xml
```xml
<servers>
    <server>
      <id>jfrog-snapshots</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
    <server>
      <id>jfrog-releases</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
  </servers>
```
### Step 4: Run the below command to push the artifacts to Jfrog Artifactory.
```sh
mvn deploy
```
### Step 5: Verify whether artifact(war) is published or not in Jfrog Artifactory.
<p align="center">
  <img width="400" src="" alt="Jfrog Artifactory output"/>
</p>
### Step 6 : Deploy the war file in Tomcat.
### Step 7 : Verify whether application is running or not

#### Congratulations. You have successfully deployed the artifact(war) file in Tomcat.
