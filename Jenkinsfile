pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'deploy-to-eks-dockerhub-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
          
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
               docker tag web-application:$BUILD_NUMBER mmreddy424/web-application:$BUILD_NUMBER
                
                '''
                
            }
        }
        stage('Push Docker Image') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub_crdenatils', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                 sh '''
                 docker login -u $DOCKER_HUB_USERNAME   -p $DOCKER_HUB_PASSWORD
                  docker push mmreddy424/web-application:$BUILD_NUMBER
                    
                   ''' 
}
            }
            
        }
        
        stage('Deployto AWS EKS') {
            steps {
                withAWS(credentials: 'AWS', region: 'us-east-1') {
  sh '''
                aws eks update-kubeconfig --name dev-cluster --region us-east-1
                cd kubernetes-yaml
                kubectl apply -f .
                
  
  '''
                    
                    
}
                
            }
        }
        
        
      
    }
}
