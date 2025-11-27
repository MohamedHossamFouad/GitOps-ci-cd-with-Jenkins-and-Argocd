pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'       
        IMAGE_NAME = 'mohamedhossam0/jenkins-nodejs:latest'  
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'Master', url: 'https://github.com/MohamedHossamFouad/GitOps-ci-cd-with-Jenkins-and-Argocd.git'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    echo 'Logging in to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        echo 'Login successful'
                    }
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    def app = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    echo 'Pushing image to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        def app = docker.image("${IMAGE_NAME}")
                        app.push('latest')
                    }
                }
            }
        }
    }
}
