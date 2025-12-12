pipeline {
    agent any

    environment {
        IMAGE = "sksahilahmed1604/devops-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE}:${BUILD_ID} ."
                    sh "docker tag ${IMAGE}:${BUILD_ID} ${IMAGE}:latest"
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh "docker push ${IMAGE}:${BUILD_ID}"
                sh "docker push ${IMAGE}:latest"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment will come next..."
            }
        }
    }
}
