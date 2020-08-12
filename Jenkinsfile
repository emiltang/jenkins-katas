pipeline {
  agent any
  stages {
    stage('Clone Down') {
      steps {
        stash(name: 'code', excludes: '.git/')
      }
    }
 
    stage('Build/Test App') {
      parallel {
        stage('Build App') {
          agent {
            docker {
              image 'gradle:jdk11'
            }
          }
          options {
            skipDefaultCheckout(true)
          }
          steps {
            unstash 'code'
            sh 'sh ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            stash(name: 'code', excludes: '.git/')
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

    stage('Push Docker') {
      environment {
        DOCKER = credentials('docker')
      }
      options {
        skipDefaultCheckout(true)
      }
      steps {
        unstash 'code'
        sh 'ci/build-docker.sh'
        sh 'echo "$DOCKER_PSW" | docker login -u "$DOCKER_USR" --password-stdin'
        sh 'ci/push-docker.sh'
      }
    }
  }
  environment {
    docker_username = 'emiltang'
  }
}
