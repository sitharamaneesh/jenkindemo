pipeline {
    agent { label 'development' }
    environment {
        DOCKER_IMAGE = 'sitharamaneesh/firstrepo'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
      stage('Build Docker image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push Docker image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }

        stage('Run Docker container') {
            steps {
                script {
                    docker.run("${DOCKER_IMAGE}:latest")
                }
            }
        }


        }
    }
