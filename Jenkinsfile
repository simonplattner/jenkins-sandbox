pipeline {

  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    durabilityHint('PERFORMANCE_OPTIMIZED')
    parallelsAlwaysFailFast()
    quietPeriod(0)
    skipDefaultCheckout()
    skipStagesAfterUnstable()
    timeout(time: 5, unit: 'MINUTES')
    timestamps()
  }

//  triggers {
//    cron('* * * * *')
//  }

  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
  }

  stages {
    stage('Parallel Stage 1') {
//      when {
//        not {
//          branch 'main'
//        }
//      }
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
//      when {
//        branch 'main'
//      }
      options {
        timeout(time: 30, unit: 'SECONDS')
      }
      input {
        message "Should we continue?"
        ok "Yes, we should."
        submitter "alice,bob"
        parameters {
          string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        }
      }
      steps {
        echo "Hello ${params.PERSON}"
        echo "Biography: ${params.BIOGRAPHY}"
        echo "Toggle: ${params.TOGGLE}"
        echo "Choice: ${params.CHOICE}"
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
              when {
                triggeredBy 'SCMTrigger'
              }
              steps {
                echo "some scm trigger!"
              }
            }
          }
        }
      }
    }
    stage('Non-Parallel Stage 2') {
      when {
        triggeredBy 'TimerTrigger'
      }
      steps {
        echo 'This stage will be executed first.'
      }
    }
  }
  post {
    success {
      echo 'test success!'
    }
    always {
      echo 'I will always say Hello again!'
    }
  }
}
