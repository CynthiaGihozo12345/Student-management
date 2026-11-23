pipeline {

    // Run on an available Jenkins agent
    agent any

    stages {

        // Stage 1: Install project dependencies
        stage('Install Dependencies') {
            steps {
                echo 'Installing project dependencies...'
                bat 'npm install'
            }
        }

        // Stage 2: Run unit tests
        stage('Unit Testing') {
            steps {
                echo 'Running unit tests...'
                bat 'npm test -- tests/unit.test.js'
            }
        }

        // Stage 3: Run integration tests
        stage('Integration Testing') {
            steps {
                echo 'Running integration tests...'
                bat 'npm test -- tests/integration.test.js'
            }
        }

        // Stage 4: Static Application Security Testing
        stage('SAST Security Scan') {
            steps {
                echo 'Scanning source code for security vulnerabilities...'

                bat '''
                docker run --rm -v "%WORKSPACE%:/src" semgrep/semgrep semgrep scan --config p/security-audit --error /src
                '''
            }
        }

        // Stage 5: Testing and security summary
        stage('Pipeline Summary') {
            steps {
                echo 'Unit tests, integration tests and SAST completed successfully!'
            }
        }
    }

    post {

        success {
            echo 'SUCCESS: All tests and security scans passed!'
        }
        failure {
            echo 'FAILURE: Tests or security scanning detected a problem!'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}
