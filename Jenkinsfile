pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'PAT_Jenkins'
        GIT_URL = 'https://github.com/ltmichael52/Git_Fundamental'
        IMAGE_NAME = 'my-nginx-app'
        CONTAINER_NAME = 'my-nginx-container'
        DEPLOY_PORT = '8081'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'loc_feature',
                    url: "${GIT_URL}",
                    credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying new container..."
                    sh """
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                        docker run -d --name ${CONTAINER_NAME} -p ${DEPLOY_PORT}:80 ${IMAGE_NAME}:latest
                    """
                }
            }
        }
    }
}

