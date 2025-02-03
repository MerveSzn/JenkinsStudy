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
                    def result = sh(script: 'npx cypress run --reporter spec', returnStdout: true)
                                echo result
                                // You can further process the result string to check for success/failure

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
