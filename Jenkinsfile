pipeline {
    agent any
    
    environment {
        AZURE_SUBSCRIPTION = credentials('your-azure-subscription-id')
        AKS_RESOURCE_GROUP = 'your-aks-resource-group'
        AKS_CLUSTER = 'your-aks-cluster'
        KUBECONFIG = credentials('your-kubeconfig-credentials-id')
    }
    
    stages {
        stage('Azure Login') {
            steps {
                script {
                    // Login to Azure
                    withCredentials([azureServicePrincipal(credentialsId: 'your-azure-service-principal-id', tenantId: 'your-azure-tenant-id', appId: 'your-azure-app-id', password: 'your-azure-password')]) {
                        sh "az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID"
                    }
                }
            }
        }
        
        stage('Set AKS Context') {
            steps {
                script {
                    // Set AKS context
                    sh "az aks get-credentials --resource-group $AKS_RESOURCE_GROUP --name $AKS_CLUSTER --overwrite-existing"
                }
            }
        }
        
        stage('Build Docker Images') {
            steps {
                script {
                    // Build Docker images
                    sh "docker-compose -f docker-compose.yaml build"
                    sh "docker-compose -f docker-compose.yaml push"
                }
            }
        }
        
        stage('Deploy to AKS') {
            steps {
                script {
                    // Deploy to AKS
                    withCredentials([file(credentialsId: 'your-kubeconfig-credentials-id', variable: 'KUBECONFIG')]) {
                        sh "export KUBECONFIG=$KUBECONFIG"
                    }
                    sh "kubectl apply -f your-kubernetes-resources.yaml"
                }
            }
        }
    }
}
