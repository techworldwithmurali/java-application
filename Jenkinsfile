pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'pushing-docker-image-to-ecr-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
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
              docker build . --tag web-application:$BUILD_NUMBER
              docker tag web-application:$BUILD_NUMBER 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
                
                '''
                
            }
        }  
      
      stage('Push Docker Image') {
          steps{
 withAWS(credentials: 'AWS', region: 'us-east-1') {
       
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 108290765801.dkr.ecr.us-east-1.amazonaws.com
                   docker push 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
                    '''
                }
            } 
            
      }
      
    }
}
