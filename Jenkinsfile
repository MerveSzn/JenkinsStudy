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
                    sh 'npx cypress run --reporter mochawesome --reporter-options reportDir=./cypress/reports,overwrite=true'
                }
            }
        }
            stage('Publish Mochawesome Report') {
                    steps {
                        script {
                            // Raporu Jenkins'e yükleyin
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
            // Başarı durumunda yapılacak işlemler
            echo 'Pipeline başarıyla tamamlandı!'
        }
        failure {
            // Hata durumunda yapılacak işlemler
            echo 'Pipeline sırasında bir hata oluştu.'
        }
    }
}