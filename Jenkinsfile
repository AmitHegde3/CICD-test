pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "CI-CD-test"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // You can add tests here
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/amithegde/cicd-test', 'dockerhub-jenkins-token') {
                        dockerImage.push()
                    }
                    sh 'docker run -d -p 3000:3000 ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }
}
