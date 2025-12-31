pipeline {
    agent any

    environment {
        IMAGE_NAME = "finalapp"
        IMAGE_TAG  = "${BUILD_NUMBER}"
        EC2_IP     = "52.66.4.150"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no ubuntu@$52.66.4.150 '
                docker stop finalapp || true &&
                docker rm finalapp || true &&
                docker run -d -p 8080:80 --name finalapp finalapp:2
                '
                """

            }
        }
    }
}
