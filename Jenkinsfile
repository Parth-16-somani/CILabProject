pipeline {
    agent any

    stages {

        stage('Build & Test - Main') {
            when {
                branch 'main'
            }
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test Only - Feature Branch') {
            when {
                branch pattern: "feature/.*", comparator: "REGEXP"
            }
            steps {
                sh 'mvn test'
            }
        }

        stage('Release Validation') {
            when {
                branch pattern: "release/.*", comparator: "REGEXP"
            }
            steps {
                sh 'mvn clean verify'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
