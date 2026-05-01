pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-html-app"
        CONTAINER_NAME = "my-container"
        PORT = "3000"
    }

    stages {

        stage('git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/muskanmohit15/jenkins-live.git'
            }
        }

        stage('docker build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Start Container') {
            steps {
                sh '''
                docker run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }


    }

}