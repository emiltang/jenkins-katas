pipeline {
  agent any
  stages {
    stage('hello') {
      steps {
        sh 'echo "Hello World"'
      }
    }

    stage('Build App') {
      agent {
        docker {
          image 'gradle:jdk11'
        }

      }
      steps {
        sh 'sh ci/build-app.sh'
        archiveArtifacts 'app/build/libs/'
      }
    }

  }
}