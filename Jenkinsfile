pipeline {
agent any

```
stages {

    stage('Build Docker Image') {
        steps {
            script {
                sh 'docker compose build'
            }
        }
    }

    stage('Run Docker Containers') {
        steps {
            script {
                sh 'docker compose up -d'
            }
        }
    }

    stage('Verify Containers') {
        steps {
            script {
                sh 'docker compose ps'
                sh 'docker compose logs --tail=50'
            }
        }
    }

    stage('Run Spark Job') {
        steps {
            script {
                sh '''
                    docker compose exec -T spark-master \
                    spark-submit /opt/spark-apps/your_spark_job.py
                '''
            }
        }
    }
}

post {
    success {
        script {
            slackSend(
                channel: '#spark-alerts',
                color: 'good',
                message: "Build SUCCESSFUL: ${env.JOB_NAME} [${env.BUILD_NUMBER}] (${env.BUILD_URL})"
            )
        }
    }

    failure {
        script {
            slackSend(
                channel: '#spark-alerts',
                color: 'danger',
                message: "Build FAILED: ${env.JOB_NAME} [${env.BUILD_NUMBER}] (${env.BUILD_URL})"
            )
        }
    }

    always {
        script {
            sh 'docker compose down'
        }
    }
}
```

}
