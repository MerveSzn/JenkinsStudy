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
                    sh 'npm ci' // Daha hızlı ve temiz kurulum için 'npm ci' kullanıldı
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
