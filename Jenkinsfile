pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t node-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker stop node-app || exit 0'
                bat 'docker rm node-app || exit 0'
                bat 'docker run -d -p 3000:3000 --name node-app node-app'
            }
        }
    }
}