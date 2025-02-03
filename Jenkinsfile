pipeline {
    agent any

    options {
        ansiColor('xterm')
    }
    environment {
        PATH = "/usr/local/bin:/opt/homebrew/bin:$PATH"
        CYPRESS_CACHE_FOLDER = "$HOME/.cache/Cypress" // Cypress cache için
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
                    sh 'npx cypress run --reporter mochawesome'
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
        always {
                    archiveArtifacts artifacts: 'cypress/results/*.json', allowEmptyArchive: true
                    publishHTML(target: [
                        reportDir: 'cypress/results',
                        reportFiles: 'mochawesome.html',
                        reportName: 'Cypress Test Report'
                    ])
                }
    }
}