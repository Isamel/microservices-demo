pipeline {
  agent {
    docker {
      image 'efx-cam/docker:18.06.1-ce'
    }

  }
  stages {
    stage('Test') {
      steps {
        sh 'docker container ls'
      }
    }
  }
}