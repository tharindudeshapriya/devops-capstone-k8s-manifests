pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/tharindudeshapriya/devops-capstone-k8s-manifests.git'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'capstone-devops-cluster', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://EABA2B1A35D888CD50C218ED96310403.gr7.us-east-1.eks.amazonaws.com') 
                {
                    sh 'kubectl apply -f k8s/Manifest.yaml -n webapps'
                    sh 'kubectl apply -f k8s/HPA.yaml'
                    sleep 30
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }
        }
        
    }