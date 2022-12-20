pipeline {

  environment {
    registry = "adefendi/api-produto"
    registryCredencial = 'dockerhub'
  }

  agent any

  stages {
    stage ('Build Image') {
      steps {
        script {
          dockerapp = docker.build("alexandre/api-produto:1.${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
        }
      }
    steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredencial) {
            dockerapp.push()
          }
        }
      }
    }
  }
}