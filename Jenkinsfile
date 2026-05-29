pipeline {

    // Define the agent to run the pipeline on 
    agent {
        label 'devops1-ahmad'
    }

    // Checkout code from GitHub repository
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ahmad-Rizki21/simple-apps.git'
            }
        }

        // Build the application
        stage('Build') {
            steps {
                sh '''cd app 
                npm install'''
            }
        }

        // Testing Apps
        stage('Testing Apps') {
            steps {
                sh '''cd app
                npm test
                npm run test:coverage'''
            }
        }

        // Code Analysis with SonarQube
        stage('Code Analysis') {
            steps {
                sh '''cd app
                sonar-scanner \
                    -Dsonar.projectKey=simple-apps \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://172.23.8.74:9000 \
                    -Dsonar.token=sqp_a548ddc19492c1c1a86c0d4ca196283b81314286'''
            }
        }

        // Deploy the application using Docker Compose
        stage('Deploy App') {
            steps {
                sh '''
                docker compose build
                docker compose up -d'''
            }
        }

    }

}