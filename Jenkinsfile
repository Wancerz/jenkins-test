pipeline {
    agent any
    environment {
        IMAGE = "jenkins-test"
        TAG = "latest"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Wancerz/jenkins-test.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE}:${TAG} ."
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                script {
                    sh """
                    kubectl delete deployment myapp || true
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                    """
                }
            }
        }
    }
}