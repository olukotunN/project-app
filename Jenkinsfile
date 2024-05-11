pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'your-docker-registry-url' // Replace with your Docker registry URL
        KUBE_CONFIG = credentials('your-kubernetes-config') // Replace with your Kubernetes config credentials ID
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('your-docker-image:latest')
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                // Add steps to run tests (e.g., npm test)
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(env.DOCKER_REGISTRY, 'docker-credentials') {
                        docker.image('your-docker-image:latest').push('latest')
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f ./kubernetes/deployment.yaml'
                    sh 'kubectl apply -f ./kubernetes/service.yaml'
                }
            }
        }
    }
}

