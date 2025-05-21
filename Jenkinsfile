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
        HELM_CHART_PATH = 'simple-web-chart/'
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
               echo "Checking if Release exits..."
               sh """
                 if helm status ${HELM_CHART} -n ${NAMESPACE} > /dev/null 2>&1; then
                    echo "Release found. Upgrading..."
                 else
                    echo "Release not found. Installing..."
                 fi
                 helm upgrade --install ${HELM_CHART} ${HELM_CHART_PATH} -n ${NAMESPACE}
                 """
               }
            }

       stage('Chart Destroy') {
           when {
               expression { params.OPTIONS == 'Destroy' }
           }
           steps {
              sh "Checking if Release exits..."
              sh """
                if helm status ${HELM_CHART} -n ${NAMESPACE} > /dev/null 2>&1; then
                   echo "Release found. Uninstalling..."
                   helm uninstall ${HELM_CHART} ${HELM_CHART_PATH} -n ${NAMESPACE}
                else
                  echo "Release does not exists."
                fi
                """
               }
            }
       }
}

