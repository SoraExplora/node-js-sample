pipeline {
    agent any

    tools {
        nodejs "NodeJS"   
    }

    environment {
        // Add any ENV vars if needed here
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Code Analysis - SonarQube') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    sh 'npx sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodejs-app:latest .'
            }
        }

        stage('Push to Nexus (Optional)') {
            steps {
                echo 'Simulate uploading to Nexus or Docker Registry'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}

