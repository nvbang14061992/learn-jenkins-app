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

        stage('tests') {
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                    a
                '''
            }
        }
    }
    
    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}
