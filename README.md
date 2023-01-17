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
Job Name: static-code-analysis
```
### Step 3: Configure the git repository
```xml
GitHub Url: https://github.com/techworldwithmurali/java-application.git
Branch : static-code-analysis-jenkinsfile
```
### Step 4: Write the Jenkinsfile
  + ### Step 4.1: Clone the repository 
```xml
stage('Clone') {
            steps {
                git branch: 'static-code-analysis-jenkinsfile', url: 'https://github.com/techworldwithmurali/java-application.git'
            }
        }
```
  + ### Step 4.2: Build and Static code Analysis
```xml
stage('Build and Analysis') {
            steps {
                sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://your_sonar_url -Dsonar.login=your_sonar_token'
            }
        }
```
     
### Step 5: Verify whether SonarQube report is generated or not in SonarQube Dashboard.

#### Congratulations. You have successfully Published the static code analysis report in SonarQube using Jenkins Pipeline job.
