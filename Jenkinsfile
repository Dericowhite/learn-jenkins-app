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
                sh'''
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('test') {
            
            steps {
                sh 'echo "Test stage...."'
                script {
                    def fileExists = fileExists 'build/index.html'
                    
                    if (fileExists) {
                        echo 'index.html exists in the build folder'
                    } else {
                        error 'index.html does not exist in the build folder'
                    }
                } 
                sh '''
                echo "Running npm tests ....."
                npm test
                ''' 
            }
        }
    }
}
