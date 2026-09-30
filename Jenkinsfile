pipeline {
    agent any

    options {
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/shaheemshahee625-lang/NodeProject.git'
                    ]],
                    extensions: [
                        [$class: 'CloneOption',
                         shallow: true,
                         depth: 1,
                         noTags: true,
                         timeout: 30]
                    ]
                ])
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }
    }
}