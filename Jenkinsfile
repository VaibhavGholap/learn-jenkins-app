pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
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
                // We start the app in the background, wait for port 3000 to be live, and then execute tests
                sh '''
                    npm start & 
                    npx wait-on http://localhost:3000
                    PLAYWRIGHT_JUNIT_OUTPUT_NAME=results.xml npx playwright test --reporter=junit
                '''
            }
        }
    }

    post {
        always {
            junit '**/results.xml'
        }
    }
}