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
                      npm  --version
                      chown -R node:node .
                      rm -rf node_modules package-lock.json
                      npm cache clean --force
                      npm install
                      npm run build
                      ls -la
                '''
            }

        }

        stage('Test'){

            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Test stage......'
            }

        }
    }
}
