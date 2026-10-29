pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin"
        KUBECONFIG = "/Users/neerajmaurya/.kube/config"
    }

    stages {
        stage('Verify Kubernetes') {
            steps {
                sh 'kubectl get nodes'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }

        stage('Wait for Rollout') {
            steps {
                sh 'kubectl rollout status deployment/lab-set02 --timeout=180s'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl get deployment lab-set02'
                sh 'kubectl get pods -l app=lab-set02 -o wide'
                sh 'kubectl describe deployment lab-set02'
            }
        }
    }

    post {
        success {
            echo 'SET 2 PASSED: Sample application deployed successfully.'
        }
        failure {
            echo 'SET 2 FAILED: Check the console output.'
        }
    }
}
