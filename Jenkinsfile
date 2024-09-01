pipeline {
    agent any

    environment {
        REDIS_CONTAINER_NAME = 'redis-server'
        REDIS_IMAGE = 'redis:6.2-alpine'
    }

    stages {
        stage('Pull Redis Image') {
            steps {
                script {
                    echo "Pulling Redis Docker image..."
                    sh "docker pull ${REDIS_IMAGE}"
                }
            }
        }

        stage('Run Redis Container') {
            steps {
                script {
                    echo "Running Redis Docker container..."
                    sh """
                        docker run -d \
                        --name ${REDIS_CONTAINER_NAME} \
                        -p 6379:6379 \
                        ${REDIS_IMAGE}
                    """
                }
            }
        }

        stage('Check Redis Status') {
            steps {
                script {
                    echo "Checking Redis container status..."
                    sh "docker ps | grep ${REDIS_CONTAINER_NAME}"
                }
            }
        }
    }
    
    post {
        success {
            script {
                echo "Redis container is up and running."
            }
        }
    }
}
