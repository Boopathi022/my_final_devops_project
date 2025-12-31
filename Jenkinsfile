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
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh """
                scp -i /home/ubuntu/mumbai-key.pem -r . ubuntu@52.66.4.150:/home/ubuntu/app
                ssh -i /home/ubuntu/mumbai-key.pem -o StrictHostKeyChecking=no ubuntu@52.66.4.150 << EOF
                cd /home/ubuntu/app
                docker build -t finalapp:$IMAGE_TAG .
                docker stop finalapp || true
                docker rm finalapp || true
                docker run -d -p 8080:80 --name finalapp finalapp:$IMAGE_TAG
                EOF
                """
           }
       }

    }
}
