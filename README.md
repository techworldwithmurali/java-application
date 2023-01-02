+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for manually building and pushing artifacts(war) to Jfrog Artifactory</br>

## Manually - Build and Push to Jfrog Artifactory

### Prerequisites:
+ Git is installed
+ Maven is installed
+ SonarQube is installed

### Step 1: Clone the repository
  
```xml
    github url: https://github.com/techworldwithmurali/java-application.git
    branch name: static-code-analysis
```

### Step 2: Update the SonarQube details in pom.xml
```xml
<dependency>
<groupId>org.sonarsource.scanner.maven</groupId>
<artifactId>sonar-maven-plugin</artifactId>
<version>3.2</version>
</dependency>

<profiles>
<profile>
<id>sonar</id>
<activation>
<activeByDefault>true</activeByDefault>
</activation>
<properties>
<!-- Optional URL to server. Default value is http://localhost:9000 -->
<sonar.host.url>
http://10.155.19.5:9000
</sonar.host.url>
</properties>
</profile>
</profiles>

```
### Step 3: Verify whether SonarQube report is generated or not in SonarQube Dashboard..
```sh
mvn sonar:sonar -Dsonar.sonar.host.url=http://13.233.6.6:9000 -Dsonar.login=a59971a4cf3ee650a17c928570ce7fb268c36a90
```
### Step 4: Verify whether SonarQube report is generated or not in SonarQube Dashboard.
<p align="center">
  <img width="400" src="https://user-images.githubusercontent.com/115227391/210243233-12497d72-52e7-4e7f-bb9d-eef7d6fadf99.png" alt="cli output"/>
</p>


#### Congratulations. You have successfully Published the static code analysis report in SonarQube..
