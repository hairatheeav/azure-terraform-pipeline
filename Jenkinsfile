pipeline {
    agent any
    
    environment {
        // Map Jenkins credentials to environment variables Terraform understands
        ARM_CLIENT_ID       = credentials('azure-client-id')
        ARM_CLIENT_SECRET   = credentials('azure-client-secret')
        ARM_SUBSCRIPTION_ID = credentials('azure-subscription-id')
        ARM_TENANT_ID       = credentials('azure-tenant-id')
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                cleanWs()
                checkout scm
            }
        }
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Terraform Apply') {
            steps {
                // Change to apply if running in production, or add an approval step
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }
}
