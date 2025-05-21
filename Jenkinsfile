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

