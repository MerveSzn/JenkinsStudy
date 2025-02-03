pipeline {
    agent any
    environment {
        PATH = "/usr/local/bin:$PATH"
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
        stage('Create Report Directory') {
            steps {
                script {
                    sh 'mkdir -p cypress/reports'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh 'npx cypress run --reporter mochawesome --reporter-options reportDir=./cypress/reports,overwrite=true'
                }
            }
        }
        stage('Publish Mochawesome Report') {
            steps {
                script {
                    // Rapor dizinini doğru şekilde kopyala
                    sh "cp -r cypress/reports ${env.WORKSPACE}/htmlreports/Cypress_20Test_20Report"
                    publishHTML(target: [
                        reportName: 'Cypress Test Report',
                        reportDir: 'cypress/reports',
                        reportFiles: 'mochawesome.html',
                        keepAll: true,
                        allowMissing: false
                    ])
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline başarıyla tamamlandı!'
        }
        failure {
            echo 'Pipeline sırasında bir hata oluştu.'
        }
    }
}