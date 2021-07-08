pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('nns15899-dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t nns15899/dp-alpine:latest .'
            }
        }
        stage('login') {
            steps { 
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | DOCKER LOGIN -U $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps{
                sh 'docker push nns15899/dp-alpine:latest'
            }           
        }

    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
