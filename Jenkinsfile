
pipeline {
    agent any

    stages {
        stage('Validate Kubernetes') {
            steps {
                bat 'kubectl version --client'
            }
        }

        stage('Deploy Application and Service') {
            steps {
                withCredentials([
                    file(credentialsId: 'kubeconfig-credentials',
                         variable: 'KUBECONFIG')
                ]) {
                    bat 'kubectl apply -f deployment.yaml'
                    bat 'kubectl rollout status deployment/set5-deployment --timeout=120s'
                }
            }
        }

        stage('Verify Service') {
            steps {
                withCredentials([
                    file(credentialsId: 'kubeconfig-credentials',
                         variable: 'KUBECONFIG')
                ]) {
                    bat 'kubectl get deployments'
                    bat 'kubectl get pods'
                    bat 'kubectl get service set5-service'
                    bat 'kubectl get endpoints set5-service'
                }
            }
        }
    }
}
