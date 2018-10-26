pipeline {
  agent {
    docker {
      image 'maven:3.5.4-jdk-8'
      args 'mvn clean'
    }

  }
  stages {
    stage('Test') {
      steps {
        sh 'mvn -v'
      }
    }
  }
}