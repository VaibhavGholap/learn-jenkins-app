pipeline {
    agent any

    stages {

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    mkdir -p build
                    touch build/index.html
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    test -f build/index.html
                    echo "index.html exists"
                '''
            }
        }
    }
}