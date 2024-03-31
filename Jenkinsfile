pipeline {
    agent any
    
    environment {
        ACR_REGISTRY = "myregistry123did.azurecr.io"
    }
    
    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Log into ACR registry
                        sh "az login"
                        sh az acr login $ACR_REGISTRY                       
                    }

                    // Build Docker image
                    sh "docker build -t $ACR_REGISTRY/your-image-name:latest ."

                    // Push Docker image
                    sh "docker push $ACR_REGISTRY/your-image-name:latest"
                }
            }
        }
    }
}
