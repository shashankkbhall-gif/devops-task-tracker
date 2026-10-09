
pipeline {
    agent any

    environment {
<<<<<<< HEAD
        image_name = "shashankshashank123/devops-task-tracker"
    }

    stages {
=======
        DOCKER_IMAGE = "shashankshashank123/devops-task-tracker"
        DOCKER_CREDENTIALS = "dockerhub-credentials"
        IMAGE_TAG = "${new Date().format('yyyy-MM-dd-HHmmss')}"
    }

    stages {

>>>>>>> 6ea2df36841ff95bcc67dd66c771c9e8f3ef69ed
        stage("git-checkout") {
            steps {
                checkout scm
            }
        }
<<<<<<< HEAD
        stage("image-build") {
            steps {
                script {
                    env.image_tag = new Date().format("yyyy-MM-dd-HHmmss")
                    env.full_image = "${env.image_name}:${env.image_tag}"
                }
            }
        }
        stage("docker login") {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
=======

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
>>>>>>> 6ea2df36841ff95bcc67dd66c771c9e8f3ef69ed
                    }
                }
            }
        }
<<<<<<< HEAD
        stage("docker push") {
            steps {
                script {
                    bat "docker build -t ${env.full_image} ."
                    bat "docker push ${env.full_image}"
=======

        stage("docker push") {
            steps {
                script {
                    bat "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
>>>>>>> 6ea2df36841ff95bcc67dd66c771c9e8f3ef69ed
                }
            }
        }
    }
}
<<<<<<< HEAD
=======

>>>>>>> 6ea2df36841ff95bcc67dd66c771c9e8f3ef69ed
