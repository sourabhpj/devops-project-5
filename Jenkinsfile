pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nginx-image .'
            }
        }
        stage('Deploy to container') {
            steps {
            sh 'docker stop my-nginx-image || true'
            sh 'docker rm my-nginx-image || true'
            sh 'docker run -d --name my-nginx-image -p 80:80 my-nginx-image'
        }
    }
}
}