+ <b>Author: Moole Muralidhara Reddy</b></br>
+ <b>Email:</b> techworldwithmurali@gmail.com</br>
+ <b>Website:</b> techworldwithmurali.com , devopsbymurali.com</br>
+ <b>Description:</b> Below are the steps outlined for Jenkins Pipeline - Static Code Analysis using SonarQube</br>

## Jenkins Pipeline - Static Code Analysis using SonarQube

### Prerequisites:
  + Jenkins is installed
  + SonarQube is installed
  + Github token generate

### Step 1: Install and configure the jenkins plugins
  + git
  + maven integration
  + SonarQube Scanner plugin
  
### Step 2: Create the Jenkins Pipeline job
```xml
Job Name: static-code-analysis-jenkins-piepline
```
### Step 3: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : static-code-analysis-jenkinsfile
```
### Step 4: Write the Jenkinsfile
  + ### Step 4.1: Clone the repository 
```xml
stage('Clone the repository'){
        steps{
          git branch: 'deploy-to-eks-jfrog-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
        } 
      }
```
  + ### Step 4.2: Build the code
```xml
stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
```
+ ### Step 4.3: Static code analysis
```xml
stage('Static code analysis') {
            steps {
        withSonarQubeEnv('Sonarqube-8.9.10') {
                    sh  "mvn sonar:sonar"
                }
                }
                
            }
```
     
### Step 5: Verify whether SonarQube report is generated or not in SonarQube Dashboard.

#### Congratulations. You have successfully Published the static code analysis report in SonarQube using Jenkins Pipeline job.
