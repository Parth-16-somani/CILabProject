pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'jdk21'
    }

    stages {

        stage('Build & Test - Main') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                mvn clean test
                '''
            }
        }

        stage('Test Only - Feature Branch') {
            when {
                branch 'feature/login'
            }
            steps {
                sh '''
                mvn test
                '''
            }
        }

        stage('Release Validation') {
            when {
                branch 'release/v1.0'
            }
            steps {
                sh '''
                mvn clean test
                '''
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
        }
    }
}
