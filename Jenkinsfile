pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "larudhanu/node-app"
        TAG = "latest"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:%TAG% .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker stop node-app || exit 0'
                bat 'docker rm node-app || exit 0'
                bat 'docker run -d -p 3000:3000 --name node-app %DOCKER_IMAGE%:%TAG%'
            }
        }
    }
<<<<<<< HEAD
}
=======
}
>>>>>>> a57a020d2633b1d07fd05d61d18163578e3d8a74
