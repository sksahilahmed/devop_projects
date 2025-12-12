pipeline {
    agent any

    environment {
        IMAGE = "sksahilahmed/devops-app"
        
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

        stage('Login to DockerHub') {
            steps {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat """
                    docker logout
                     docker login -u %USER% -p %PASS%
                     """
                     }
                 }
        }

        stage('Deploy') {
            steps {
                echo "Deployment will come next..."
            }
        }
    }
}
