pipeline {
    agent any // Jenkins sunucusunda herhangi bir ajan kullanılacak
    environment {
        // Ortam değişkenleri burada tanımlanabilir
        PATH = "/usr/local/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Git reposundan en son sürümü çekiyoruz
                    checkout scm
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Gerekli bağımlılıkları yüklüyoruz
                    sh 'npm install'
                    sh 'npm install mochawesome mochawesome-report-generator cypress'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Cypress testlerini çalıştırıyoruz
                    sh 'npx cypress run'
                }
            }
        }
        stage('Generate Report') {
            steps {
                script {
                    // Mochawesome raporunu oluşturuyoruz
                    sh 'npx mochawesome-merge cypress/results/*.json > cypress/results/merged-report.json'
                    sh 'npx mochawesome-report-generator cypress/results/merged-report.json'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Uygulamanın dağıtımını gerçekleştiriyoruz
                    sh 'npm run deploy'
                }
            }
        }
    }
    post {
        success {
            // Başarı durumunda yapılacak işlemler
            echo 'Pipeline başarıyla tamamlandı!'
        }
        failure {
            // Hata durumunda yapılacak işlemler
            echo 'Pipeline sırasında bir hata oluştu.'
        }
    }
}