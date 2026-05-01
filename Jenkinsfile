pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-html-app"
        CONTAINER_NAME = "my-container"
        PORT = "3000"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME} .
                """
            }
        }

        stage('Stop Old Container') {
            steps {
                sh """
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                """
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker run -d -p ${PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}
                """
            }
        }
    }
}