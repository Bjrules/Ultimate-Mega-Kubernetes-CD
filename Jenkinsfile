pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'gitpass', url: 'https://github.com/Bjrules/Ultimate-Mega-Kubernetes-CD.git'
            }
        }
        
        stage('Kubernetes Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'bbanjo-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://952FB702C508F688D873376083B31DF5.gr7.ap-south-1.eks.amazonaws.com') {
                    sh "kubectl apply -f Manifest/manifest.yaml -n webapps"
                    sh "kubectl apply -f Manifest/HPA.yaml "
                    sleep 30
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get service -n webapps"
                }
            }
        }
    }
}
