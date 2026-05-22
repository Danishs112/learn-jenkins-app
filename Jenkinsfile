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
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
            agent {
                docker {
                    image  'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm --version
                npm ci
                npm test
                '''
            }
        }

        stage('Verify test'){
            steps {
                sh '''
                test -f build/index.html
                '''
            }
        }
    }
}