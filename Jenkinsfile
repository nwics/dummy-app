pipeline {
  agent any
  environment {
    DOCKER_IMAGE = 'nabilwics/dummy-app'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          bat 'docker build -t %DOCKER_IMAGE% ./deployment'
        }
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-credentials',  // ID credential di Jenkins
          usernameVariable: 'DOCKER_USER',         // Nama variable untuk username
          passwordVariable: 'DOCKER_PASS'          // Nama variable untuk password
        )]) {
          bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
          bat 'docker push %DOCKER_IMAGE%'
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat 'kubectl apply -f deployment/kubernetes/deployment.yaml'
      }
    }
  }
}
