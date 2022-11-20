pipeline {
    agentany 

    stages {
        steps ( 'Git Checkout') {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ma1456/EKS-CICD.git']]])
        }
    }
}