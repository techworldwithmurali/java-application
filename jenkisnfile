pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }

    stages {
        stage('Clone the repository') {
            steps {
               git branch: 'build-and-deploy-to-tomcat-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/techworldwithmurali/java-application.git'
            }
        }
        
        stage('Build the code') {
            steps {
            sh 'mvn clean install'
                
            }
        }
        
        stage('Deploy to tomcat') {
            steps {
            deploy adapters: [tomcat7(credentialsId: 'Tomcat-7-cred', path: '', url: 'http://100.25.166.179:8080')], contextPath: null, war: '**/*.war'
                
            }
        }
    }
}
