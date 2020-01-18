pipeline {
  agent any
  stages {
    stage('Build Docker') {
      steps {
        sh '''pipeline {
  agent any
  stages {
    stage(\'Build Docker\') {
      steps {
        sh \'make build\'
      }
    }'''
        }
      }
      stage('Lint') {
        steps {
          sh 'make lint'
        }
      }
      stage('Login to dockerhub') {
        steps {
          withCredentials(bindings: [string(credentialsId: 'docker-pwd', variable: 'dockerhubpwd')]) {
            sh 'docker login -u mjpraino -p ${dockerhubcredentials}'
          }

        }
      }
      stage('Upload Image') {
        steps {
          sh 'make upload'
        }
      }
      stage('Deploy Kubernetes') {
        steps {
          sh 'kubectl apply -f ./kubernetes'
        }
      }
    }
  }