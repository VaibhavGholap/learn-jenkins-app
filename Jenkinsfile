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
                // Set the output path for the junit report explicitly
                sh 'PLAYWRIGHT_JUNIT_OUTPUT_NAME=results.xml npx playwright test --reporter=junit'
            }
        }
    }

    post {
        // FIXED: Added the required conditional block (always)
        always {
            // FIXED: Pointed to the correct root or relative location where the XML is generated
            junit '**/results.xml'
        }
    }
}