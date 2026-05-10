pipeline {
    agent any
    stages {
        stage("checkout code"){
            steps{
                   checkout scm
            }
        }
        stage("Build"){
            steps{
                    sh 'docker build -t my-nginx-image .'
            }
        }
        stage("Deploy"){
            steps{
                   sh 'docker stop my-nginx-image || true'
                   sh 'docker rm my-nginx-image || true'
                   sh 'docker run -d --name my-nginx-image -p 80:80 my-nginx-image'
            }
        }
        
    }
}