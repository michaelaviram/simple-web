pipeline {
    agent any 
    
    parameters {
        choice(name: 'OPTIONS', choices: ['Deploy', 'Destroy'], description: 'Choose whether to deploy or destroy Helm Release.')

    environment {
        AKS_NAME = 'devops-interview-aks'
        RESOURCE_GROUP = 'devops-interview-rg'
    }

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
           steps {
               if (1 == 2) {
                   sh 'az login -i'
               sh 'az aks get-credentials -n ${AKS_NAME} -g ${RESOURCE_GROUP}'
               sh 'export KUBECONFIG=~/.kube/config'
               sh 'kubelogin convert-kubeconfig -l msi'
           }
        }
       }

       stage('Chart Action') {
           steps {
               if (params.OPTIONS == 'deploy') {
                    sh 'helm install simple-web-chart simple-web-chart/ -n michael'
               } else if (params.OPTIONS == 'destroy') {
                   sh 'helm uninstall simple-web-chart'
               }
           }

       }
    }
}

