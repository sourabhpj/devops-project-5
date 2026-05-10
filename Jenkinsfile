pipeline {
    agent any
    stages {
        stage("checkout"){
            steps{
                    sh 'git scm'
            }
        }
        stage(){
            steps{
                sh 'docker build -t sourabh-img .'
            }
        }
        stage("Deploy"){
            steps{
                sh 'docker stop sourabh-img || true'
                sh 'docker rm sourabh-img || true'
                sh 'docker run -d --name sourabh-img -p 80:80 sourabh-img'
            }
        }
    }
}