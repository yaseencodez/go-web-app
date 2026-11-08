pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/yaseencodez/go-web-app.git'
            }
        }

        stage('Build Go Application') {
            steps {
                echo 'Building Go application'
                sh 'go version'
                sh 'go build -o main .'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t mdyaseenh/go-web-app:v2 .'
            }
        }
    }
}
