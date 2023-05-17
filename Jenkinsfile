pipeline {
    agent { label 'development' }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Docker Build & Push') {
            steps {
                echo "Starting Dockerbuild"
                sh "/usr/local/bin/aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 721983679407.dkr.ecr.us-east-1.amazonaws.com"
                sh "docker build -t jenkins_docker_ec2 ."
                sh "docker tag jenkins_docker_ec2:latest 721983679407.dkr.ecr.us-east-1.amazonaws.com/jenkins_docker_ec2:latest"
                sh "docker push 721983679407.dkr.ecr.us-east-1.amazonaws.com/jenkins_docker_ec2:latest"
            }
        }

        stage('Docker Run') {
            steps {

                echo "Starting Docker run.."
                sh "docker run -d 721983679407.dkr.ecr.us-east-1.amazonaws.com/jenkins_docker_ec2:latest"
            }
            }
        }
    }
