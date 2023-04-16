pipeline {
    agent any
    stages{
        stage ('Build Docker Image'){
            steps {
                script {
                    dockerapp = docker.build("pestana1984/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

    }

}