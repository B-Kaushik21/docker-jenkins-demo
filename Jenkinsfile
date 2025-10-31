pipeline {
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = 'kaushik021/docker-jenkins-demo'
    }

    stages {
        stage('checkout source code') {
            steps {
                echo 'Pulling source code from GitHub...'
                git branch: 'master', url: 'https://github.com/B-Kaushik21/docker-jenkins-demo.git'
            }
        }

        stage('build docker image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('login to dockerhub') {
            steps {
                bat '''
                echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin
                '''
            }
        }

        stage('push docker image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Docker image pushed successfully to Docker Hub!'
        }
        failure {
            echo '❌ Docker image push failed'
        }
    }
}
