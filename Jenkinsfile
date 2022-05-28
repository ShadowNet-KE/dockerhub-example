pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t buluma/dp-alpine:latest .'
            }
        }
        stage('login') {
            steps { 
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | DOCKER LOGIN -U $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps{
                sh 'docker push buluma/dp-alpine:latest'
            }           
        }

    }
//     post {
//         always {
//             sh 'docker logout'
//         }
//     }
}
