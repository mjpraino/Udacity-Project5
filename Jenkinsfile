pipeline {
  agent any
  stages {
    stage('Build Docker') {
      steps {
        sh 'make build'
      }
    }
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }
    stage('Login to dockerhub') {
      steps {
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerhubpwd')]) {
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
