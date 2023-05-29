pipeline {
    agent { label 'development' }
    environment {
        DOCKER_IMAGE = 'sitharamaneesh/firstrepo'
	tag = sh(returnStdout: true, script: "git rev-parse --short=10 HEAD").trim()
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
                    docker.build("${DOCKER_IMAGE}:${tag}")
                }
            }
        }

        stage('Push Docker image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("${DOCKER_IMAGE}:${tag}").push()
                    }
                }
            }
        }

       stage('Run Docker container') {
            steps {
                script {
		    def containerName = "apachesite" 
		    sh "docker stop ${containerName} || true"
		    sh "docker rm ${containerName} || true"
                    sh "docker run -d --net=host ${DOCKER_IMAGE}:${tag}"
                }
            }
        }


        }
    }
