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
        stage('Run Tests') {
            steps {
                script {
                    sh 'npx cypress run'
                }
            }
        }
        stage('Publish Mochawesome Report') {
            steps {
                script {
                    // Rapor dizinini oluşturun
                    sh 'mkdir -p cypress/reports'

                    // Raporu doğru dizine kopyalayın
                    archiveArtifacts allowEmptyArchive: true, artifacts: '**/cypress/reports/**/*'

                    // HTML raporunu yayınla
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
