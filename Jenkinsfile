pipeline {

    // Define the Jenkins agent using a Docker container
    agent {
        docker {
            // Use the Node.js 18 Alpine image
            image 'node:18-alpine'

            // Reuse the same workspace on the Jenkins node
            reuseNode true
        }
    }

    stages {

        stage('Install Dependencies') {
            steps {
                // Install all dependencies from package-lock.json
                sh 'npm ci'
            }
        }

        stage('Build') {
            steps {
                // Create a build directory and a sample index.html file
                sh '''
                    mkdir -p build
                    touch build/index.html
                '''
            }
        }

        stage('Test') {
            steps {
                // Execute test cases defined in package.json
                sh 'npm test'
            }
        }
    }

    post {

        // Actions that run regardless of pipeline result
        always {

            // Publish JUnit test results in Jenkins
            junit 'test-results/junit.xml'
        }
    }
}