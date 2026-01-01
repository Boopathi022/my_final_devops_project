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

        stage('Copy Code to EC2') {
            steps {
                sh '''
                rsync -av --exclude='.git' \
                -e "ssh -i ${SSH_KEY} -o StrictHostKeyChecking=no" \
                ./ ubuntu@${EC2_IP}:/home/ubuntu/app
                '''
            }
        }

        stage('Build & Run on EC2') {
            steps {
                sh '''
ssh -i ${SSH_KEY} -o StrictHostKeyChecking=no ubuntu@${EC2_IP} << EOF
cd /home/ubuntu/app
docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} .
docker stop myapp || true
docker rm myapp || true
docker run -d -p 8081:80 --name myapp ${IMAGE_NAME}:${IMAGE_VERSION}
EOF
                '''
            }
        }
    }
}

