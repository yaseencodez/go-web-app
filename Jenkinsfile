
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mdyaseenh/go-web-app'
        DOCKER_TAG = 'v1'
    }

    stages {

        stage('Welcome') {
            steps {
                echo 'Welcome to Go Web App CI/CD!'
            }
        }

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub.'
            }
        }

        stage('Check Go') {
            steps {
                sh 'go version'
            }
        }

        stage('Build Go Application') {
            steps {
                sh 'go build -o app .'
            }
        }

        stage('Docker Version') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check Console Output.'
        }
    }
}

