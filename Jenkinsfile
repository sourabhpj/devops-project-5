pipeline {
    agent any
    stages {
        stage('Checkout') {
            step {
                git scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nginx-image .'
            }
        }
        stage('Deploy to container') {
            sh 'docker stop my-nginx-container || true'
            sh 'docker rm my-nginx-container || true'
            sh 'docker run -d --name my-nginx-container -p 80:80 my-nginx-image'
        }
    }
}