pipeline {

  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }

  stages {

    stage('Build') {

      steps {
        sh 'docker build -t janibehm/quote-generator:latest .'
      }
    }

    stage('Login') {

      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {

      steps {
        sh 'docker push janibehm/quote-generator:latest'
      }
    }
  }

}