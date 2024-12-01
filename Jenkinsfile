pipeline {
    agent any

    environment {
        INDEX_FILE_NAME = 'build/index.html'
    }

    stages {
        /*
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u root' // Run the container as root
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        */

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u root' // Run the container as root
                }
            }
            steps {
                sh '''
                    echo "Test stage"
                    test -f $INDEX_FILE_NAME
                    npm test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}