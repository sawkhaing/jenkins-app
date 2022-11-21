pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                docker build . -t test
            }
        }
    }
}