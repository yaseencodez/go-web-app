
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

        stage('Docker Login and Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                            --username "$DOCKER_USERNAME" \
                            --password-stdin

                        docker push ${DOCKER_IMAGE}:${DOCKER_TAG}

                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Go application built and Docker image pushed to Docker Hub!'
        }

        failure {
            echo 'FAILURE: Pipeline failed. Check Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}

