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
            sh 'npm run test:unit'  // Vue test command
          }
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        script {
          sh '''
            curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
            chmod +x kubectl
            mv kubectl /usr/local/bin/
          '''
          sh 'kubectl apply -f k8s-deployment.yml'
        }
      }
    }
  }
}