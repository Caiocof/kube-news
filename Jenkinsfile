pipeline {
    agent any

    stages{
        stage ('Build Docker Image'){
            steps{
                script{
                    dockerapp = docker.build("caiocof/kube-news:${env.BUILD_ID}", '-f ./Dockerfile .')
                }
            }
        }
    }
}