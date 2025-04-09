pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-node-web'
        CONTAINER_NAME = 'jenkins-node-container'
        CONTAINER_PORT = '80'
        HOST_PORT = '80'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "📥 Cloning source code..."
                git 'https://github.com/ATHITHYAN-V/Jenkins-pipelines.git'  
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "🐳 Building Docker image..."
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo "🚀 Deploying Docker container..."
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p $HOST_PORT:$CONTAINER_PORT $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful! Visit: http://$HOSTNAME:$HOST_PORT"
        }
        failure {
            echo "❌ Deployment Failed! Check logs."
        }
    }
}
