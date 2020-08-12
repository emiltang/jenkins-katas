pipeline {
  agent any
  stages {
    stage('Clone Down') {
      steps {
        stash(name: 'code', excludes: '.git/')
      }
    }

    stage('Build App') {
      parallel {
        stage('Build App') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            skipDefaultCheckout true
            unstash 'code'
            sh 'sh ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

        stage('Test App') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'sh ci/unit-test-app.sh'
            junit 'app/build/test-results/test/TEST-*.xml'
          }
        }

      }
    }

  }
}