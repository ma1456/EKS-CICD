pipeline {
    tools {
        maven 'Maven3'
    }
    agent any 

    stages {
        stage ( 'Git Checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ma1456/EKS-CICD.git']]])
           }
        }
        stage ( ' Build ') {
            steps {
                sh 'mvn clean install'
            }
        }
        
    }
}