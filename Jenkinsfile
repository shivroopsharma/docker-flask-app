pipeline {
  agent any
  environment {
    DOCKER_CREDENTIALS = credentials('dockerhub-creds')
    IMAGE_NAME = "shivroop/flask-docker-app"
  }
  stages {
    stage('Checkout Code') {
      steps {
        git url: 'https://github.com/shivroopsharma/docker-flask-app.git', branch: 'main'
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${IMAGE_NAME}")
        }
      }
    }
    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
            docker.image("${IMAGE_NAME}").push()
          }
        }
      }
    }
  }
}
