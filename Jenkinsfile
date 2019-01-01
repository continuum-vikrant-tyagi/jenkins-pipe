pipeline {
    agent none
    stages {
        
        stage('node-go') {
            agent {
                docker { image 'go:3.8-alpine' }
            }
            steps {
                sh 'go version'
                sh 'echo $GOPATH'
            }
        }
    }
}
