pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Test') {
      steps {
        script {
          docker.image('node:16').inside {
            sh 'npm install'
            sh 'npm test'  // Vue test command
          }
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
          sh 'kubectl apply -f k8s-deployment.yml'
        }
      }
    
  }
}