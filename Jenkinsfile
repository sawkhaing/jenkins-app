pipeline {
    options {
        disableConcurrentBuilds()
    }
    agent {
        kubernetes {
            defaultContainer 'docker-client'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  name: dind
spec:
  serviceAccountName: jenkins
  containers:
  - name: docker-client
    image: docker:stable-dind
    command: ['sleep', '99d']
    env:
    - name: DOCKER_HOST
      value: tcp://localhost:2375
  - name: docker-daemon
    image: docker:stable-dind
    env:
    - name: DOCKER_TLS_CERTDIR
      value: ""
    securityContext:
      privileged: true
    volumeMounts:
      - name: cache
        mountPath: /var/lib/docker
  - name: helm
    image: alpine/helm:3.10.2
    command:
    - cat
    tty: true
  volumes:
  - name: cache
    hostPath:
      path: /tmp
      type: Directory
"""
        }
    }
    environment {
        
    }
    stages {
        stage('Checkout scm') {
            steps {
                checkout scm
            }
        }
        stage('Docker Build') {
            steps {
                container('docker-client') {
                    withCredentials([file(credentialsId: 'docker-credentials', variable: 'DOCKER_CONFIG_JSON')]) {
                        sh '''
                            mkdir -p $HOME/.docker/
                            cp $DOCKER_CONFIG_JSON /$HOME/.docker/config.json
                            ls -al $HOME/.docker/
                            docker version
                        '''
                        sh '''
                            docker build . -t sawkhaing/azt-nginx:1.0.0
                            docker push sawkhaing/azt-nginx:1.0.0
                       '''
                    }
                }
            }
        }
        stage('helm') {
          steps {
            container('helm') {
              sh 'helm install azt-nginx ./helm-charts --create-namespace --namespace app'
            }
          }
        }
    }
}