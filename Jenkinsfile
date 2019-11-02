pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:6-alpine'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh ' npm install'
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('deliver') {
      parallel {
        stage('deliver') {
          steps {
            sh ' ./jenkins/scripts/deliver.sh'
            input '"Proceed" to continue'
            sh './jenkins/scripts/kill.sh'
          }
        }
        stage('Deploy') {
          steps {
            sh 'npn install'
          }
        }
      }
    }
  }
  environment {
    CI = 'true'
  }
}