pipeline {
  agent {
    label "private"
  }
  options {
    timeout(30)
  }
  stages {
    stage('Deploy') {
      steps {
        dir('deployment') {
          steps {
            script {
              withCredentials([string(credentialsId: 'eksCert', variable: 'eksCert')]) {
                kubeconfig(caCertificate: "${eksCert}", credentialsId: 'ecr:us-east-1:qtran', serverUrl: 'https://B23528C720C4ECB9BF5C320A8D6776C4.gr7.us-east-1.eks.amazonaws.com') {
                  kubectl apply -f .
                }
              }
            }
          }
        }
      }
    }
  }
}