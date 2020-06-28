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
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: 'Harbor-1', url:'harbor-1.nubeliu.com') {
          sh 'docker push harbor-1.nubeliu.com/teco/worker'
        }
      }
    }
  }
}
