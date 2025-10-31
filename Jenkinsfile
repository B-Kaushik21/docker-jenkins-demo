pipeline {
    agent any 
    enviroment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
        IMAGE_NAME = 'kaushik021/docker-jenkins-demo'
    }
    stages{
        stage('checkout source code'){
            steps{
                echo 'pulling source code from github'
                git branch: 'main', url: 'https://github.com/B-Kaushik21/docker-jenkins-demo.git'
            }
        }
        stage('build docker image'){
            steps{
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }
        stage('login to dockerhub'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push docker image'){
            steps{
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }

    post{
        success{
            echo 'docker image pushed successfully'
        }
        failure{
            echo 'docker image push failed'
        }
    }
}