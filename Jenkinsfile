pipeline {
    agent any

    stages{
        stage ('Build Docker Image'){
            steps{
                script{
                    dockerapp = docker.build("caiocof/kube-news:${env.BUILD_ID}", '-f ./Dockerfile .')
                }
            }
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }
}