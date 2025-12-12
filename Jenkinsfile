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
                bat "docker build -t %IMAGE%:%BUILD_ID% ."
                bat "docker tag %IMAGE%:%BUILD_ID% %IMAGE%:latest"
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat """
                    echo %PASS% | docker login -u %USER% --password-stdin
                    """
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                bat "docker push %IMAGE%:%BUILD_ID%"
                bat "docker push %IMAGE%:latest"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment will come next..."
            }
        }
    }
}
