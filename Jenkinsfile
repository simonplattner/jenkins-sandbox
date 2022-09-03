pipeline {

  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '1', artifactNumToKeepStr: '1'))
    skipDefaultCheckout()
    skipStagesAfterUnstable()
    timeout(time: 5, unit: 'MINUTES')
  }

  stages {
    stage('Parallel Stage 1') {
      parallel {
        stage('Branch A') {
          steps {
            echo "On Branch A"
          }
        }
        stage('Branch B') {
          steps {
            echo "On Branch B"
          }
        }
        stage('Branch C') {
          stages {
            stage('Nested 1') {
              steps {
                echo "In stage Nested 1 within Branch C"
              }
            }
            stage('Nested 2') {
              steps {
                echo "In stage Nested 2 within Branch C"
              }
            }
          }
        }
      }
    }
    stage('Non-Parallel Stage 1') {
      steps {
        echo 'This stage will be executed first.'
      }
    }
    stage('Parallel Stage 2') {
      parallel {
        stage('Branch A') {
          steps {
            echo "On Branch A"
          }
        }
        stage('Branch B') {
          steps {
            echo "On Branch B"
          }
        }
        stage('Branch C') {
          stages {
            stage('Nested 1') {
              steps {
                echo "In stage Nested 1 within Branch C"
              }
            }
            stage('Nested 2') {
              steps {
                echo "In stage Nested 2 within Branch C"
              }
            }
          }
        }
      }
    }
    stage('Non-Parallel Stage 2') {
      steps {
        echo 'This stage will be executed first.'
      }
    }
  }
}
