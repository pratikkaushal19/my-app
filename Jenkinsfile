pipeline {
 agent any

 environment {
  IMAGE_NAME = "pratikkaushal/myapp"
 }

 stages {
stage('Clone Source') {
 steps {
  git branch: 'main', url: 'https://github.com/pratikkaushal19/my-app.git'
 }
}

  stage('Build Docker Image') {
   steps {
    sh 'docker build -t $IMAGE_NAME:latest .'
   }
  }

  stage('Login to Docker Hub') {
 steps {
  withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
   sh '''
   echo $DOCKER_TOKEN | docker login -u pratikkaushal --password-stdin
   '''
  }
 }
}

  stage('Push to Docker Hub') {
 steps {
  sh 'docker push pratikkaushal/myapp:latest'
 }
}
 }
}