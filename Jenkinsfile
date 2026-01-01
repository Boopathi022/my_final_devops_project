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
                sh '''
                rsync -av --exclude='.git' \
                -e "ssh -i /home/ubuntu/mumbai-key.pem -o StrictHostKeyChecking=no" \
                ./ ubuntu@52.66.4.150:/home/ubuntu/app
                '''
            }
        }

    }
}

