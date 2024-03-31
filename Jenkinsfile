pipeline {
    agent any
    
    environment {
        ACR_REGISTRY = "myregistry123did.azurecr.io"
    }
    
    stages {
        stage('Build Image') {
            steps {
                script {
                    // Build Docker image
                       sh "docker -t build Dockerfile ."

                    // Push Docker image
                    // sh "docker push $ACR_REGISTRY/your-image-name:latest"
                }
            }
        }
    }
}
