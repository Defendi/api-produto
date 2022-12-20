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
          dockerapp = docker.build(registry + ":1.${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
        }
      }
    }
    stage ('Push Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredencial) {
            dockerapp.push('latest')
            dockerapp.push("1.${env.BUILD_ID}")
          }
        }
      }
    }
    stage ('Deploy Kubernets') {
      steps {
        withKubeConfig([credentialId: 'kubeconfig']) {
          sh 'kubectl apply -f ./k8s/deployment.yaml'
        }
      }
    }
  }
}