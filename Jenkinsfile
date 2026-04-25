pipeline {
    agent any

    environment {
        IMAGE_NAME = "pratikkaushal19/myapp"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh """
                    echo \$DOCKER_TOKEN | docker login -u pratikkaushal19 --password-stdin
                    """
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }

    }
}