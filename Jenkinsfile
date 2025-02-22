pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Jenkins-docker')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t hemanth990/my-app:latest .'
      }
    }
    stage('Login') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Jenkins-docker', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
          sh "echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin"
        }
      }
    }  // **Closing brace added here**
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

