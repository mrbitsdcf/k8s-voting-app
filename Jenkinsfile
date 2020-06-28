pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/result:kube${BUILD_NUMBER} ./result'
      }
    }
    stage('Build vote') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/vote:kube${BUILD_NUMBER} ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/worker:kube${BUILD_NUMBER} ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'https://harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/result:kube${BUILD_NUMBER}'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'https://harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/vote:kube${BUILD_NUMBER}'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'https://harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/worker:kube${BUILD_NUMBER}'
        }
      }
    }
    stage('Deploy result image') {
      steps {
        sh "kubectl set image deployment/result result=push harbor-1.nubeliu.com/teco/worker:kube${BUILD_NUMBER}"
      }
    }
  }
}
