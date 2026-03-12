pipeline {
    agent any

    environment {
        NODE_VERSION = "22" // match your repo's Node.js version
    }

    triggers {
        pollSCM('H/1 * * * * *')  // Poll for changes every 1 seconds
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/RanitMondal03/APIPlay.git'
            }
        }

        stage('Setup NODtyjuyE') {
            steps {
                tool name: "NodeJS ${NODE_VERSION}", type: 'NodeJS'
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
                sh 'npx playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test'
            }
        }
    }

    post {
        always {
            // Archive Playwright report
            archiveArtifacts artifacts: 'playwright-report/**', allowEmptyArchive: true
        }
        success {
            echo 'All tests passed!'
        }
        failure {
            echo 'Some tests failed!'
        }
    }
}
