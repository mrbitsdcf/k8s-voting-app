pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/result ./result'
      }
    }
    stage('Build vote') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t harbor-1.nubeliu.com/teco/worker ./worker'
      }
    }
    stage('Push result image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'') {
          sh 'docker push harbor-1.nubeliu.com/teco/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'') {
          sh 'docker push harbor-1.nubeliu.com/teco/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'') {
          sh 'docker push harbor-1.nubeliu.com/teco/worker'
        }
      }
    }
  }
}
