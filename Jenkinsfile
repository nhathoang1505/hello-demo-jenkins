pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                bat 'docker build -t hello-jenkins .'
            }
        }

        stage('Test Docker') {
            steps {
                bat 'docker ps -a'
            }
        }

        stage('Deploy (Run Container)') {
            steps {
                // Stop container cũ nếu có (tránh lỗi "port already allocated")
                bat '''
                docker stop hello-jenkins-container || echo "No container to stop"
                docker rm hello-jenkins-container || echo "No container to remove"
                '''

                // Chạy container mới
                bat 'docker run -d --name hello-jenkins-container -p 8081:8080 hello-jenkins'
            }
        }
    }
}
