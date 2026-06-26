pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.54.2-jammy'
            reuseNode true
        }
    }

    stages {
        stage('Install') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npx playwright test --reporter=junit'
            }
        }
    }

    post {
         {
            junit 'test-results/*.xml'
        }
    }
}