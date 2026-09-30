pipeline {
    agent any

    stages {

        stage('Check Node') {
            steps {
                bat 'node --version'
                bat 'npm --version'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    bat 'npm ci'
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir('backend') {
                    bat 'echo No backend tests configured yet'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    bat 'npm ci'
                }
            }
        }

        stage('Test Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm run test --if-present'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm run build'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }

        failure {
            echo 'Build or tests failed.'
        }

        always {
            archiveArtifacts artifacts: 'frontend/dist/**',
                             allowEmptyArchive: true
        }
    }
}