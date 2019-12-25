pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        gitHubPRStatus githubPRMessage('${GITHUB_PR_COND_REF} build started')
        githubPRAddLabels labelProperty: labels('jenkins'), statusVerifier: allowRunOnStatus('SUCCESS'), errorHandler: statusOnPublisherError('FAILURE')
        sh 'mvn -B clean package -DskipTests'
      }
    }

    stage('Test') {
      steps {
        gitHubPRStatus githubPRMessage('${GITHUB_PR_COND_REF} tests started')
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
    stage('Finalisation') {
      steps {
        gitHubPRStatus githubPRMessage('${GITHUB_PR_COND_REF} build ended')
        githubPRComment comment: githubPRMessage('Build ${BUILD_NUMBER} ${BUILD_STATUS}'), errorHandler: statusOnPublisherError('FAILURE'), statusVerifier: allowRunOnStatus('SUCCESS')
        githubPRStatusPublisher buildMessage: message(failureMsg: githubPRMessage('Can\'t set status; build failed.'), successMsg: githubPRMessage('Can\'t set status; build succeeded.')), statusMsg: githubPRMessage('${GITHUB_PR_COND_REF} run ended'), unstableAs: 'FAILURE', statusVerifier: allowRunOnStatus('SUCCESS'), errorHandler: statusOnPublisherError('FAILURE')
      }
    }
  }
  tools {
    maven 'maven 3.6.3'
  }
}