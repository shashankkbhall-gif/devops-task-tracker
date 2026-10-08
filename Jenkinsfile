
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "shashankshashank123/devops-task-tracker"
        DOCKER_CREDENTIALS = "dockerhub-credentials"
        IMAGE_TAG = "${new Date().format('yyyy-MM-dd-HHmmss')}"
    }

    stages {

        stage("git-checkout") {
            steps {
                checkout scm
            }
        }

        stage("image-build") {
            steps {
                script {
                    bat "docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} ."
                }
            }
        }

        stage("docker login") {
            steps {
                script {
                    withCredentials([
                        usernamePassword(
                            credentialsId: "dockerhub-credentials",
                            usernameVariable: "DOCKER_USERNAME",
                            passwordVariable: "DOCKER_PASSWORD"
                        )
                    ]) {
                        bat '''
                            echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
                        '''
                    }
                }
            }
        }

        stage("docker push") {
            steps {
                script {
                    bat "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
                }
            }
        }
    }
}
```
