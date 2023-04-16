pipeline {
    agent any

    stages {
        stage ('Build Docker Image'){
            steps {
                script {
                    dockerapp = docker.build("pestana1984/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Docker Image'){
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy Kubernetes'){
            steps {
                withKubeconfig([credentialsId: 'KubeConfig']){
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }

        }
    }
}