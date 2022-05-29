pipeline {
    agent { label 'dind-1.0.0' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('985ac3d1-8c9e-461f-8f0c-489ab96cb40b')
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
