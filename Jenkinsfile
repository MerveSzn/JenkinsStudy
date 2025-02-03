pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
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
                    sh 'npm install'
                    sh 'npm install mochawesome mochawesome-report-generator cypress'
               }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npx cypress run --reporter spec --browser chrome --headless'
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
