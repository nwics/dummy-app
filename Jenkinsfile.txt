pipeline {
  agent any
  environment {
    DOCKER_IMAGE = 'nabilwics/dummy-app'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          sh 'docker build -t $DOCKER_IMAGE ./deployment'
        }
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-credentials',
          usernameVariable: 'nabilwics',
          passwordVariable: '54173qwe'
        )]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          sh 'docker push $DOCKER_IMAGE'
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment/kubernetes/deployment.yaml'
      }
    }
  }
}
