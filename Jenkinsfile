pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t myflask:test .'
            }
        }
        stage('Verify') {
            steps {
                sh 'docker images | grep myflask'
            }
        }
    }
}
