pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'GitHub-Access', url: 'https://github.com/Bjrules/Ultimate-Mega-Kubernetes-CD.git'
            }
        }
        
        stage('Kubernetes Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'bb-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://DEC9982C055F2774BBB4E534B90AD5AC.sk1.us-east-1.eks.amazonaws.com') {
                    sh "kubectl apply -f Manifest/manifest.yaml"
                    sh "kubectl apply -f Manifest/HPA.yaml"
                    sleep 30
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get service -n webapps"
                }
            }
        }
    }
}
