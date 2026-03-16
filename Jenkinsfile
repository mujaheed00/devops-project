pipeline {
    agent any
    environment {
        DOCKERHUB_CREDS = credentials('dockerhub-credentials')
    }
    stages {
        stage('Push Docker Images') {
            steps {
                bat """
                echo %DOCKERHUB_CREDS_PSW% | docker login -u %DOCKERHUB_CREDS_USR% --password-stdin
                docker push %DOCKERHUB_CREDS_USR%/frontend:latest
                docker push %DOCKERHUB_CREDS_USR%/backend:latest
                """
            }
        }
    }
}
