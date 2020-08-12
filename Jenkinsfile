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
        sh '''cd ci

&& ./build-app.sh'''
      }
    }

  }
}