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
                sh 'docker build -t devops-cicd-demo:v1 .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker image inspect devops-cicd-demo:v1'
                echo 'Docker image test passed'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f devops-cicd-container || true
                    docker run -d --name devops-cicd-container -p 8080:80 devops-cicd-demo:v1
                '''
            }
        }
    }
}
