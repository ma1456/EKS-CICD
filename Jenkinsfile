pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    environment {
        registry = "923954127216.dkr.ecr.us-east-2.amazonaws.com/manojrepository"
    }
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
        stage ( 'Build Docker Image') {
            steps {
                script {
                    docker build registry
                }
            }
        }
        
    }
}    
