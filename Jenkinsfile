pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-id')
        IMAGE_NAME = 'maira555/ci-cd-demo-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/maira148/ci-cd-demo-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        docker.image("${IMAGE_NAME}").push("latest")
                    }
                }
            }
        }
    }
}

