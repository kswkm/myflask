pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build Image') {
      steps { sh 'docker build -t myflask:${BUILD_NUMBER} .' }
    }
    stage('Verify') {
      steps { sh 'docker images | grep myflask' }
    }
    stage('Deploy') {
      steps {
        sh '''
          docker save myflask:${BUILD_NUMBER} | docker exec -i minikube docker load
          kubectl apply -f k8s/
          kubectl set image deployment/myflask myflask=myflask:${BUILD_NUMBER}
          kubectl rollout status deployment/myflask --timeout=120s
          kubectl get pods
        '''
      }
    }
  }
}
