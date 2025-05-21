pipeline {
    agent any 

    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Clean') {
            steps {
               cleanWs()
            }
        }

        stage('Fetch') {
            steps {
                echo "Fetch Stage"
                checkout scm
            }
       }

       stage('Connect to Cluster') {
           teps {
               sh 'az aks get-credentials -n devops-interview-aks -g  devops-interview-rg'
               sh 'export KUBECONFIG=~/.kube/config'
               sh 'kubelogin convert-kubeconfig -l msi'
           }
       }

       stage('Deploy Chart') {
           steps {
               sh 'helm install simple-web-chart simple-web-chart/ -n michael'
           }
       }
    }
}

