pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_USER = "tata197"
        IMAGE_NAME = "simple-app"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/tatajulistap-wq/simple-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_USER}/${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials') {
                        docker.image("${DOCKERHUB_USER}/${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and Push successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
