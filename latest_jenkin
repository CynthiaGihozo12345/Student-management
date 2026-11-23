
pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing testing dependencies...'

                sh 'node --version'
                sh 'npm --version'
                sh 'npm install'

                echo 'Dependencies installed successfully!'
            }
        }

        stage('Unit Testing') {
            steps {
                echo 'Running unit tests...'

                sh 'chmod +x node_modules/.bin/jest'
                sh 'node node_modules/jest/bin/jest.js tests/unit.test.js --runInBand'

                echo 'Unit tests completed successfully!'
            }
        }

        stage('Integration Testing') {
            steps {
                echo 'Running integration tests...'

                sh 'chmod +x node_modules/.bin/jest'
                sh 'npm run test:integration'

                echo 'Integration tests completed successfully!'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Checking Docker version...'

                sh 'docker --version'

                echo 'Building Docker image...'

                sh 'docker build -t devops-app:1.0 .'

                echo 'Docker image build completed!'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: All tests passed and Docker image built successfully!'
        }

        failure {
            echo 'FAILURE: Pipeline failed. Check the Jenkins Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution finished.'
        }
    }
}
