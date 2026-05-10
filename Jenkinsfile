pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // GitHub varun tumcha latest code ghenyasathi
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                // Dockerfile vaprun local image build karne
                sh 'docker build -t my-nginx-image .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Jenkins credentials 'dockerhub-id' madhun tumcha username ani token uchelne
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-id', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        
                        // Docker Hub var login karne
                        sh "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
                        
                        // Tumchya 'sourabhpj94' ya account sathi image tag karne
                        sh "docker tag my-nginx-image ${DOCKER_HUB_USERNAME}/my-nginx-image:latest"
                        
                        // Docker Hub var upload (push) karne
                        sh "docker push ${DOCKER_HUB_USERNAME}/my-nginx-image:latest"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Junna container stop karun naveen image run karne
                sh 'docker stop my-nginx-image || true'
                sh 'docker rm my-nginx-image || true'
                sh 'docker run -d --name my-nginx-image -p 80:80 my-nginx-image'
            }
        }
    }
}