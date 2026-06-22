pipeline {
agent any

```
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

    stage('Verify Containers') {
        steps {
            sh 'docker compose ps'
            sh 'docker compose logs --tail=50'
        }
    }

}

post {

    success {
        echo 'Pipeline completed successfully'

        slackSend(
            channel: '#spark-alerts',
            color: 'good',
            message: "Build SUCCESSFUL: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        )
    }

    failure {
        echo 'Pipeline failed'

        slackSend(
            channel: '#spark-alerts',
            color: 'danger',
            message: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        )
    }

    always {
        sh 'docker compose down'
    }
}
```

}
