pipeline {
  agent {
    docker {
      image 'efx-cam/docker:18.06.1-ce'
    }

  }
  stages {
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh '''export DOCKER_CERT_PATH=/opt/app-root/src/.docker/
export DOCKER_HOST=tcp://ec2-34-229-22-87.compute-1.amazonaws.com:2376
export DOCKER_TLS_VERIFY=1
 docker service create --name registry --publish published=5000,target=5000 registry:2'''
          }
        }
        stage('error') {
          steps {
            sh '''export DOCKER_CERT_PATH=/opt/app-root/src/.docker/






export DOCKER_HOST=tcp://ec2-34-229-22-87.compute-1.amazonaws.com:2376
export DOCKER_TLS_VERIFY=1

 '''
          }
        }
      }
    }
  }
}