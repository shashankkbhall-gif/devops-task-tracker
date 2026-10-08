pipeline {
    agent any

    environment {
        IMAGE_NAME = "shashankshashank123/devops-task-tracker"
    }

    stages {

        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Build Docker Image") {
            steps {
                bat "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        stage("Docker Login") {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat "echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin"
                }
            }
        }

        stage("Push Docker Image") {
            steps {
                bat "docker push %IMAGE_NAME%:latest"
            }
        }
    }
}