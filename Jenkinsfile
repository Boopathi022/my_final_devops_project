pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_VERSION = "${BUILD_NUMBER}"
        EC2_IP = "52.66.4.150"
        SSH_KEY = "/home/ubuntu/mumbai-key.pem"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh """
                # Copy project to EC2
                scp -i ${SSH_KEY} -o StrictHostKeyChecking=no -r . ubuntu@${EC2_IP}:/home/ubuntu/app

                # Build & run Docker on EC2
                ssh -i ${SSH_KEY} -o StrictHostKeyChecking=no ubuntu@${EC2_IP} '
                  cd /home/ubuntu/app &&
                  docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} . &&
                  docker stop ${IMAGE_NAME} || true &&
                  docker rm ${IMAGE_NAME} || true &&
                  docker run -d -p 8081:80 --name ${IMAGE_NAME} ${IMAGE_NAME}:${IMAGE_VERSION}
                '
                """
            }
        }
    }
}

