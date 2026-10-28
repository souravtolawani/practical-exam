pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
                echo 'Code fetched from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t practical-web:latest .'
            }
        }

        stage('Test Docker Image') {
            steps {
                bat 'docker image inspect practical-web:latest'
                echo 'Docker image test successful'
            }
        }

        stage('Deploy Web Application') {
            steps {
                bat 'docker rm -f practical-web 2>NUL || ver >NUL'
                bat 'docker run -d --name practical-web -p 8081:80 practical-web:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'docker ps --filter "name=practical-web"'
                echo 'Deployment completed'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}