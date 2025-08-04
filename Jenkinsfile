pipeline {
  agent any
  environment {
    DOCKER_IMAGE = 'frizz123/mendix-app:latest'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          bat "docker build -t %DOCKER_IMAGE% ./deployment"
        }
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'docker-cred-id',
          usernameVariable: 'DOCKER_USER',
          passwordVariable: 'DOCKER_PASS'
        )]) {
          bat "echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin"
          bat "docker push %DOCKER_IMAGE%"
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat "kubectl apply -f deployment/kubernetes/deployment.yaml"
      }
    }
  }
}
