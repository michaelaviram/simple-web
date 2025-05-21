pipeline {
    agent any 
    
    parameters {
        choice(name: 'OPTIONS', choices: ['Deploy', 'Destroy'], description: 'Choose whether to deploy or destroy Helm Release.')
    }

    environment {
        AKS_NAME = 'devops-interview-aks'
        RESOURCE_GROUP = 'devops-interview-rg'
        NAMESPACE = 'michael'
        HELM_CHART = 'simple-web'
        HELM_CHART_LOCATION = 'simple-web-chart/'
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
               expression { params.OPTIONS == 'Deploy' }
           }
           steps {
               sh 'helm install ${HELM_CHART} ${HELM_CHART_PATH} -n ${NAMESPACE}'
               }
            }

       stage('Chart Destroy') {
           when {
               expression { params.OPTIONS == 'Destroy' }
           }
           steps {
              sh 'helm uninstall ${HELM_CHART} ${HELM_CHART_PATH} -n ${NAMESPACE}'
               }
            }
       }
}

