pipeline {
  agent {
    docker {
      image 'efx-cam/docker:18.06.1-ce'
    }

  }
  stages {
    stage('Test') {
      steps {
        sh 'docker -H ec2-34-229-22-87.compute-1.amazonaws.com:2376 container ls'
      }
    }
  }
}