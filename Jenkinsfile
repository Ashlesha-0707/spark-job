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

    stage('Check Containers') {
        steps {
            sh 'docker compose ps'
            sh 'docker compose logs --tail=50'
        }
    }
}

post {

    success {
        echo 'Build completed successfully'
    }

    failure {
        echo 'Build failed'
    }

    always {
        sh 'docker compose down'
    }
}
```

}
