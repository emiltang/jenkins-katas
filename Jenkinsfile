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
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts 'app/build/libs/'
      }
    }

  }
}