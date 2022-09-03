pipeline {

  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '1', artifactNumToKeepStr: '1'))
    skipDefaultCheckout()
    skipStagesAfterUnstable()
    timeout(time: 5, unit: 'MINUTES')
  }

  stages {
    stage('Build') {
      steps {
        sh "echo hello build"
      }
    }
    stage('Test') {
      steps {
        sh "echo hello build"
      }
    }
    stage('Deploy') {
      steps {
        sh "echo hello build"
      }
    }
  }
}
