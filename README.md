+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually building and pushing artifacts(war) to Jfrog Artifactory</br>

## Manually - Build and Push to Jfrog Artifactory

### Prerequisites:
+ Git is installed
+ Maven is installed
+ Jfrog Artifactory is installed
+ Create maven repository in Jfrog

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
      <password>Techworld@2580</password>
    </server>
    <server>
      <id>jfrog-releases</id>
      <username>moole</username>
      <password>Techworld@2580</password>
    </server>
  </servers>
```
### Step 6: Run the below command to push the artifacts to Jfrog Artifactory.
```sh
mvn deploy
```
### Step 7: Verify whether artifact(war) is published or not in Jfrog Artifactory.


#### Congratulations. You have successfully published the artifact(war) file in Jfrog repository.
