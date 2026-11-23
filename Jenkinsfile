pipeline {

    // Execute this pipeline on any available Jenkins agent
    agent any

    stages {

        // Stage 1: Install testing dependencies
        stage('Install Dependencies') {
            steps {

                echo 'Installing testing dependencies...'

                bat 'npm ci'

                echo 'Dependencies installed successfully!'
            }
        }

        // Stage 2: Test HTML files
        stage('Unit Testing') {
            steps {

                echo 'Testing HTML page existence and structure...'

                bat 'npm run test:unit'

                echo 'Unit tests completed successfully!'
            }
        }

        // Stage 3: Test HTTP accessibility
        stage('Integration Testing') {
            steps {

                echo 'Testing HTML pages through HTTP server...'

                bat 'npm run test:integration'

                echo 'Integration tests completed successfully!'
            }
        }

        // Stage 4: Build Docker image
        stage('Build') {
            steps {

                echo 'Starting DevOps application build...'

                bat 'docker --version'

                bat 'docker build -t devops-app:1.0 .'

                echo 'Docker image build completed!'
            }
        }
    }

    post {

        success {
            echo 'SUCCESS: All HTML tests passed and Docker image built.'
        }

        failure {
            echo 'FAILURE: Check the Jenkins Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution finished.'
        }
    }
}
