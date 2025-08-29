pipeline {
  agent any
  triggers { pollSCM('H/2 * * * *') } // tạm thời: 2 phút check 1 lần; sau chuyển sang webhook
  stages {
    stage('Checkout') {
      steps { checkout scm } // kéo code từ repo đã khai báo
    }
    stage('Build image') {
      steps {
        sh 'docker build -t hello-app:latest .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm hello-app:latest npm test'
      }
    }
    stage('Deploy (run container)') {
      steps {
        sh '''
          docker rm -f hello-app || true
          docker run -d --name hello-app -p 8081:8081 hello-app:latest
        '''
      }
    }
  }
  post {
    always { echo "Done. Visit http://localhost:8081" }
  }
}
