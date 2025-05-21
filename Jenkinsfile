pipeline {
    agent any 
    
    parameters {
        choice(name: 'OPTIONS', choices: ['Deploy', 'Destroy'], description: 'Choose whether to deploy or destroy Helm Release.')
    }

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

       stage('Chart Deploy') {
           when {
               expression { params.OPTIONS == 'deploy' }
           }
           steps {
               sh 'helm install simple-web-chart simple-web-chart/ -n michael'
               }
            }

       stage('Chart Destroy') {
           when {
               expression { params.OPTIONS == 'destroy' }
           }
           steps {
              sh 'helm uninstall simple-web-chart'
               }
            }


       }
}

