pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Check Containers') {
            steps {
                sh 'docker compose ps'
                sh 'docker compose logs --tail=50'
            }
        }
    }

    post {
        always {
            sh 'docker compose down'
        }
    }
}
