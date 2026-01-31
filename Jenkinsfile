pipeline {
    agent any

    stages {

        stage('Info') {
            steps {
                echo "Branch Name: ${env.BRANCH_NAME}"
                echo "Pipeline started successfully"
            }
        }

        stage('Build - Main') {
            when {
                branch 'main'
            }
            steps {
                echo "Running full CI pipeline for MAIN branch"
            }
        }

        stage('Test - Feature & Main') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                }
            }
            steps {
                echo "Running tests"
            }
        }

        stage('Release Checks') {
            when {
                branch pattern: "release/.*", comparator: "REGEXP"
            }
            steps {
                echo "Running release validation and security checks"
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
