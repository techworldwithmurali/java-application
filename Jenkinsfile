pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'pushing-docker-image-to-jfrog-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
        } 
      }
      
  stage('Build the code') {
            steps {
                sh 'mvn clean install'
            }
        }    
    stage('Build Docker Image') {
            steps {
                sh '''
              docker build . --tag web-app:latest
              docker tag web-app:latest a0alrhqhzjivs.jfrog.io/web-application/web-app:latest
                
                '''
                
            }
        }
    
      
         

      
    }
}
