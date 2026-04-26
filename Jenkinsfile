pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "redliner240/ullas"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/redliner360/ullas.git'
            }
        }

        // ✅ LOGIN FIRST
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat "docker login -u %USER% -p %PASS%"
                }
            }
        }

        // ✅ THEN BUILD
        stage('Build Image') {
            steps {
                bat "docker build -t redliner240/ullas:latest ."
            }
        }

        // ✅ THEN PUSH
        stage('Push Image') {
            steps {
                bat "docker push redliner240/ullas:latest"
            }
        }
    }
}