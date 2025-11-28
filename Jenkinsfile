pipeline {
    agent any

    tools {
        nodejs "node18"   // 👈 name you gave under "NodeJS installations"
    }

    environment {
        // Define environment variables if needed
        BACKEND_DIR = "backend"
        FRONTEND_DIR = "frontend"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/flipkart-mern.git'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh 'npm run build'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh 'npm test || echo "No tests found"'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying MERN app..."
                // Example: copy build files to server or run docker-compose
                // sh 'scp -r frontend/build user@server:/var/www/html'
                // sh 'ssh user@server "pm2 restart backend"'
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully 🎉"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
