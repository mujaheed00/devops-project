pipeline {
    agent any

    environment {
        DOCKERHUB_CREDS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Push Docker Images') {
            steps {
                // Login to Docker Hub
                sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
                
                // Push frontend & backend images
                sh 'docker push $DOCKERHUB_CREDS_USR/frontend:latest'
                sh 'docker push $DOCKERHUB_CREDS_USR/backend:latest'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
