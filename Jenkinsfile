pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\nodejs;${env.PATH}"
    }

    stages {

        stage('Check Node.js') {
            steps {
                bat '''
                    echo Checking Node.js...
                    node --version
                    npm --version
                '''
            }
        }

        stage('Install Backend') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Install Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm install'
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
}