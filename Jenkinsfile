pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p build
                    touch build/index.html
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
    }

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }

}