pipeline {
  agent any
  stages {
    stage('hello') {
      steps {
        sh 'echo "Hello World"'
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
            sh 'sh ci/build-app.sh'
          }
        }

        stage('') {
          steps {
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}