pipeline {
    agent any
    
    environment {
        ACR_REGISTRY = "myregistry123did.azurecr.io"
        AKS_RESOURCE_GROUP = "aks-rg"
        AKS_CLUSTER = "my-aks"
        KUBECONFIG = credentials('az aks get-credentials --resource-group aks-rg --name my-aks --overwrite-existing')
    }
    
    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Log in to Azure Container Registry
                    withCredentials([usernamePassword(credentialsId: 'your-acr-credentials-id', usernameVariable: 'ACR_USER', passwordVariable: 'ACR_PASS')]) {
                        sh "docker login -u $ACR_USER -p $ACR_PASS $DOCKER_REGISTRY"
                    }
                    
                    // Build and push Docker image
                    sh "docker build -t $DOCKER_REGISTRY/your-image-name:latest ."
                    sh "docker push $DOCKER_REGISTRY/your-image-name:latest"
                }
            }
        }
        
        stage('Deploy to AKS') {
            steps {
                script {
                    // Set KUBECONFIG
                    withCredentials([file(credentialsId: 'your-kubeconfig-credentials-id', variable: 'KUBECONFIG')]) {
                        sh "export KUBECONFIG=$KUBECONFIG"
                    }
                    
                    // Deploy to AKS
                    sh "kubectl apply -f your-kubernetes-manifest.yaml"
                }
            }
        }
    }
}
