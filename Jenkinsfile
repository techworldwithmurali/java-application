pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'deploy-to-eks-jfrog-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
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
              docker build . --tag web-app:$BUILD_NUMBER
              docker tag web-app:$BUILD_NUMBER devopsmurali.jfrog.io/web-application/web-app:$BUILD_NUMBER
                
                '''
                
            }
        }
    
 stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'Jfrog-credentails', passwordVariable: 'JFROG_PASSWORD', usernameVariable: 'JFROG_USERNAME')]) {
       
                    sh '''
                    docker login -u $JFROG_USERNAME -p $JFROG_PASSWORD devopsmurali.jfrog.io
                        docker push devopsmurali.jfrog.io/web-application/web-app:$BUILD_NUMBER
                    '''
                }
            } 
            
        }     
         

      
    }
}
