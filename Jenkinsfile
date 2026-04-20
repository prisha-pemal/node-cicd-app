pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "yourdockerhubusername/node-app"
        TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                // Pull latest code from GitHub
                git 'https://github.com/prisha-pemal/node-cicd-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node modules
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Add tests if available
                echo "No tests configured"
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t $DOCKER_IMAGE:$TAG .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                // Login using Jenkins credentials
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u yourdockerhubusername --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push image to Docker Hub
                sh 'docker push $DOCKER_IMAGE:$TAG'
            }
        }

        stage('Deploy Container') {
            steps {
                // Stop old container
                sh 'docker stop node-app || true'
                sh 'docker rm node-app || true'

                // Run new container
                sh 'docker run -d -p 3000:3000 --name node-app $DOCKER_IMAGE:$TAG'
            }
        }
    }
}
