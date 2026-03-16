environment {
    DOCKERHUB_CREDS = credentials('dockerhub-credentials')
}

stages {
    stage('Push Docker Images') {
        steps {
            sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
            sh 'docker push $DOCKERHUB_CREDS_USR/frontend:latest'
            sh 'docker push $DOCKERHUB_CREDS_USR/backend:latest'
        }
    }
}
