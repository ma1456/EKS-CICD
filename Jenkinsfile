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
        stage ( ' Build Jar') {
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
        stage (' Push into ECR') {
            steps{
                sh "aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 923954127216.dkr.ecr.us-east-2.amazonaws.com"
                sh "docker push 923954127216.dkr.ecr.us-east-2.amazonaws.com/manojrepository:latest"
            }
        }
        stage ( 'K8S Deploy ') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'K8S', namespace: '', serverUrl: '') {
                    sh "kubectl apply -f eks-k8s-deployment.yaml"
                }
            }
        }
        
    }
}    
