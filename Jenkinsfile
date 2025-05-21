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

       stage('Deploy Chart') {
           steps {
               sh 'helm install simple-web-chart simple-web-chart/ -n michael'
           }
       }
    }
}

