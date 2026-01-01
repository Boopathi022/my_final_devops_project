pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_VERSION = "${BUILD_NUMBER}"
    }

    stages {
        stage('Clean Workspace') {
            steps {
                sh 'rm -rf *'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                ssh ubuntu@52.66.4.150 "
                docker stop myapp || true
                docker rm myapp || true
                docker run -d -p 8081:80 --name myapp ${IMAGE_NAME}:${IMAGE_VERSION}
                "
                '''
            }
        }
    }
}
