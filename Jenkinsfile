pipeline {
    agent any

    stages {
        stage('Build') {
            agent { dockerfile true }
            steps {
                sh 'docker build . -t test'
            }
        }
    }
}