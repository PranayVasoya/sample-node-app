// Jenkinsfile for a Node.js application
pipeline {
    agent any // Or specify a Docker agent if you have one configured

    // The 'tools' section is not needed for this Docker-based approach,
    // as the build environment is defined by the Docker image itself.

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from SCM (e.g., Git)
                // ⚠️ REPLACE THE URL BELOW WITH YOUR ACTUAL PATH ⚠️
                git branch: 'main', url: 'file:///C:/Users/Pranay/Desktop/sample-node-app'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Use a Docker image for the build environment
                    docker.image('node:18-alpine').inside {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Use the same Docker image for testing
                    docker.image('node:18-alpine').inside {
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Docker Build Application Image') {
            steps {
                script {
                    // Build a Docker image for your application
                    sh 'docker build -t my-node-app:latest .'
                }
            }
        }

        stage('Deploy (Simulated)') {
            steps {
                script {
                    // Simulate deployment by running the Docker image
                    sh 'docker stop my-node-app-container || true' // Stop if already running
                    sh 'docker rm my-node-app-container || true'  // Remove if exists
                    sh 'docker run -d --name my-node-app-container -p 3001:3000 my-node-app:latest'
                    echo "Application deployed and running on http://localhost:3001"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}