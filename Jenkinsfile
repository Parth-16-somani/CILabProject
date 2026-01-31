pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out source code"
                checkout scm
            }
        }

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                echo "Running full build for MAIN branch"
                sh 'echo "Build successful for main branch"'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                    branch pattern: "release/.*", comparator: "REGEXP"
                }
            }
            steps {
                echo "Running tests"
                sh 'echo "All tests passed"'
            }
        }

        stage('Security Scan') {
            when {
                branch pattern: "release/.*", comparator: "REGEXP"
            }
            steps {
                echo "Running security scan for release branch"
                sh 'echo "No vulnerabilities found"'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
