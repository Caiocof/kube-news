pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("caiocof/kube-news:${env.BUILD_ID}", '-f ./Dockerfile .')
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                withKubeConfig([credentialsId:'kubeconfig']) {
                    sh 'kubectl apply -f ./k8s/deployments.yaml'
                }
            }
        }
    }
}
