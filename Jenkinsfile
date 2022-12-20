pipeline {
  agent any

  stages {
    stage ('Build Image') {
      steps {
        script {
          dockerapp = docker.build("alexandre/api-produto", '-f ./src/Dockerfile ./src')
        }
      }
    }
  }
}