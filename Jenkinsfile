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
            environment {
                CI = 'false' // Prevent build failure on warnings
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version

                    # Correct permissions
                    chown -R node:node .

                    # Clean install without removing package-lock.json
                    rm -rf node_modules
                    npm cache clean --force
                    npm ci

                    # Build the app
                    npm run build

                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            environment {
                CI = 'false' // Again, override CI behavior
            }
            steps {
                echo 'Test stage......'
                sh 'npm run test --if-present'
            }
        }
    }
}