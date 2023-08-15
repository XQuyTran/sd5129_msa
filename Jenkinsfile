pipeline {
  agent any
  options {
    timeout(time: 1, unit: 'HOURS')
  }
  stages {
    stage('Build') {
      failFast true
      parallel {
        stage('Build backend') {
          steps {
            dir('src/backend') {
              script {
                backend = docker.build("massamplebackend")
              }  
            }
          }
        }
        stage('Build frontend') {
          steps {
            dir('src/frontend') {
              script{
                frontend = docker.build("massamplefrontend")
              }
            }
          }
        }
      }
    }
    stage("ecrPush") {
      steps {
        script {
          docker.withRegistry('063439157700.dkr.ecr.us-east-1.amazonaws.com', 'qtran') {
            backend.push("${env.BUILD_NUMBER}")
            backend.push("latest")

            frontend.push("${env.BUILD_NUMBER}")
            frontend.push("latest")
          }
        }
      }
    }
  }
}