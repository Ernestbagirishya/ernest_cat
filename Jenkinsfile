pipeline {
    agent any
    environment {
        IMAGE_NAME = "ernestbagirishya23/ernest:v6"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ernestbagirishya/ernest_cat.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }
        stage('Automated Testing') {
            steps {
                bat 'docker run --rm %IMAGE_NAME% node -v'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %IMAGE_NAME%'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                bat 'wsl kubectl apply -f deployment.yaml'
                bat 'wsl kubectl apply -f service.yaml'
            }
        }
    }
}
