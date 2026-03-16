pipeline {
    agent any

    environment {
        DOCKERHUB_USER = credentials('mujaheed00')
        DOCKERHUB_PASS = credentials('Mujaheed2#')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://bitbucket.org/username/repo.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build frontend image
                    sh 'docker build -t $DOCKERHUB_USER/frontend:latest ./frontend'
                    // Build backend image
                    sh 'docker build -t $DOCKERHUB_USER/backend:latest ./backend'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin'
                    sh 'docker push $DOCKERHUB_USER/frontend:latest'
                    sh 'docker push $DOCKERHUB_USER/backend:latest'
                }
            }
        }

        stage('Terraform Deploy') {
            steps {
                dir('terraform') {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                dir('k8s') {
                    sh 'kubectl apply -f .'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
