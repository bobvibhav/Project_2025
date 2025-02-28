pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('bob-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/bobvibhav/Project_2025.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t bobvibhav/gymimage:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push bobvibhav/gymimage:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
