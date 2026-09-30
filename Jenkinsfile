pipeline {
    agent any

    options {
        timeout(time: 45, unit: 'MINUTES')
        disableConcurrentBuilds()

        buildDiscarder(
            logRotator(
                numToKeepStr: '10',
                artifactNumToKeepStr: '5'
            )
        )
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out Git repository...'

                deleteDir()

                retry(3) {
                    checkout([
                        $class: 'GitSCM',

                        branches: [[
                            name: '*/main'
                        ]],

                        userRemoteConfigs: [[
                            url: 'https://github.com/shaheemshahee625-lang/NodeProject.git'
                        ]],

                        extensions: [[
                            $class: 'CloneOption',
                            shallow: true,
                            depth: 1,
                            noTags: true,
                            timeout: 30
                        ]]
                    ])
                }
            }
        }

        stage('Verify Node.js') {
            steps {
                bat '''
                    echo ==============================
                    echo Node.js version
                    echo ==============================
                    node --version

                    echo ==============================
                    echo NPM version
                    echo ==============================
                    npm --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    echo ==============================
                    echo Installing dependencies
                    echo ==============================

                    if exist package-lock.json (
                        npm ci
                    ) else (
                        npm install
                    )
                '''
            }
        }

        stage('Build') {
            steps {
                bat '''
                    echo ==============================
                    echo Building application
                    echo ==============================

                    if exist package.json (
                        npm run build --if-present
                    ) else (
                        echo package.json not found
                        exit /b 1
                    )
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                    echo ==============================
                    echo Running tests
                    echo ==============================

                    npm test --if-present
                '''
            }
        }
    }

    post {
        success {
            echo '======================================'
            echo ' Jenkins build SUCCESS'
            echo '======================================'
        }

        failure {
            echo '======================================'
            echo ' Jenkins build FAILED'
            echo '======================================'
        }

        always {
            echo 'Build completed.'
        }
    }
}