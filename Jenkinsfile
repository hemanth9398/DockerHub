pipeline {
  agent {label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Dockerhub')
  }
  stages {
    stage('gitclone'){
      steps{
        git 'https://github.com/hemanth9398/DockerHub.git'

      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t hemanth990/DockerHub:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push hemanth990/my-app:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}