pipeline {
  environment {
    registry = "starcraft66/tdude-status"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Build Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }
    stage('Push Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('cleanup') {
      steps{
        sh "docker rmi $registry:latest"
        cleanWs()
      }
    }
  }
}

