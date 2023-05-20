pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDS = credentials('docker-hub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t swamy877/jenkins .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push swamy877/jenkins'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}