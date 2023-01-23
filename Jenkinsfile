pipeline {
    agent {
        docker {
            image 'node:18.13.0-buster-slim' 
            args '-p 4000:4000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan eksekusi pipeline ke tahap Deploy, atau klik "Abort untuk menghentikan eksekusi pipeline)'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}