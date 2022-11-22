pipeline {
    agent {
        docker { image 'docker:stable-dind' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'docker ps -a'
            }
        }
    }
}