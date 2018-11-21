pipeline {
  agent {
    docker {
      image 'efx-cam/docker:18.06.1-ce'
    }

  }
  stages {
    stage('Environment Test') {
      parallel {
        stage('Docker Test ') {
          steps {
            sh 'docker -v'
          }
        }
        stage('Swarm Test') {
          steps {
            sh '''export DOCKER_CERT_PATH=/opt/app-root/src/.docker/
export DOCKER_HOST=tcp://ec2-34-229-22-87.compute-1.amazonaws.com:2376
export DOCKER_TLS_VERIFY=1
 docker node inspect self --pretty'''
          }
        }
        stage('Maven Test') {
          agent {
            docker {
              image 'ec2-35-153-204-172.compute-1.amazonaws.com:9041/efx-cam/maven:3.6.0'
            }

          }
          steps {
            sh 'mvn -v'
          }
        }
      }
    }
    stage('Compile') {
      agent {
        docker {
          image 'ec2-35-153-204-172.compute-1.amazonaws.com:9041/efx-cam/maven:3.6.0'
        }

      }
      steps {
        sh 'mvn clean'
        sh 'mvn validate'
        sh 'mvn compile'
        stash(name: 'App', includes: '**')
      }
    }
    stage('Unit Test') {
      agent {
        docker {
          image 'ec2-35-153-204-172.compute-1.amazonaws.com:9041/efx-cam/maven:3.6.0'
        }

      }
      steps {
        unstash 'App'
        sh 'mvn test'
        sh 'mvn package'
        stash(name: 'Package-App', includes: 'target/**/*')
      }
    }
    stage('SonarQube') {
      agent {
        docker {
          image 'ec2-35-153-204-172.compute-1.amazonaws.com:9041/efx-cam/maven:3.6.0'
        }

      }
      steps {
        unstash 'Packager-App'
        sh 'mvn sonar:sonar'
      }
    }
  }
}