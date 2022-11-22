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
  volumes:
  - name: cache
    hostPath:
      path: /tmp
      type: Directory
"""
        }
    }
    environment {
        IMAGE_PUSH_DESTINATION="kyounger/dind-jenkins:k8s-secret-declarative"
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
                    sh 'docker build . -t sawkhaing/azt-nginx:1.0.0'
                    }
                }
            }
        }
    }
}