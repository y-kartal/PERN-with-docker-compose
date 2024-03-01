pipeline {
    agent any
    stages {
        stage('Deploy the App') {
            steps {
                echo 'Deploy the App'
                sh 'ls -l'
                sh 'docker --version'
                sh 'docker-compose build' // Docker Compose ile projeyi oluştur
            }
        }
        stage('Destroy the infrastructure') {
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve terminate'
                }
                sh 'docker-compose down' // Docker Compose ile altyapıyı kaldır
            }
        }
    }
    post {
        success {
            script {
                slackSend channel: '#class-chat', color: '#439FE0', message: ' :100: Project-207 with jenkins :100:', teamDomain: 'devops15tr', tokenCredentialId: 'jenkins-slack'
            }
        }
    }
}
