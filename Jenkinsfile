pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B clean package -DskipTests'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Tests results') {
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