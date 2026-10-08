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
                script {
                    env.IMAGE_TAG = new Date().format("yyyy-MM-dd-HHmmss")
                    env.FULL_IMAGE = "${env.IMAGE_NAME}:${env.IMAGE_TAG}"

                    bat "docker build -t ${env.FULL_IMAGE} ."
                    bat "docker tag ${env.FULL_IMAGE} ${env.IMAGE_NAME}:latest"
                }
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

        stage("Docker Push") {
            steps {
                bat "docker push %FULL_IMAGE%"
                bat "docker push %IMAGE_NAME%:latest"
            }
        }
    }
}