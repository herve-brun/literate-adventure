pipeline {

  tools {
    maven "maven 3.6.3"
  }

  agent any

  stages {
    stage('build') {
      steps {
        sh "mvn -B clean install"
      }
    }
  }

  post {
    always {
        junit 'target/surefire-reports/**/*.xml'
    }
  }
}