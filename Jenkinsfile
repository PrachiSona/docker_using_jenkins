pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'docker_hub_credential'
        IMAGE_NAME = 'prachisonavane/assign_11'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/PrachiSona/docker_using_jenkins.git'
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        def app = docker.build("${IMAGE_NAME}:latest")
                        app.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built and pushed successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
    }
}
