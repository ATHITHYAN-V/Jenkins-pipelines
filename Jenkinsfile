pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-pipeline-test'
        DOCKER_HUB_USER = 'athithyan402'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ATHITHYAN-V/Jenkins-pipelines.git'

            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_USER}/${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials-id') {
                        docker.image("${DOCKER_HUB_USER}/${IMAGE_NAME}").push('latest')
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker rmi ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest || true"
            }
        }
    }
}
