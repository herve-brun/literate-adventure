pipeline {
  agent none
  stages {
    stage('build') {
      steps {
        tool 'maven 3.6.3'
        sh 'mvn clean package'
      }
    }

  }
}