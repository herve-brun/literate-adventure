pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'mvn -B clean package -DskipTests'
      }
    }

    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco()
        }

      }
      steps {
        sh 'mvn test'
      }
    }

    stage('JaCoCo') {
      parallel {
        stage('JaCoCo') {
          steps {
            jacoco()
          }
        }

        stage('Junit') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }

      }
    }

  }
  tools {
    maven 'maven 3.6.3'
  }
}