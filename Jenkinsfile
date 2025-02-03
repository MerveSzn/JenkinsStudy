pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/opt/homebrew/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm ci'
                    sh 'npm install'
                    sh 'npm install mochawesome mochawesome-report-generator cypress'
               }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npx cypress run --reporter spec --no-color'
                }
            }
        }


    }

    post {

        success {
            echo '✅ Pipeline başarıyla tamamlandı!'
        }
        failure {
            echo '❌ Pipeline sırasında bir hata oluştu.'
        }
    }
}
