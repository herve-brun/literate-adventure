pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        node(label: 'mynode')
        ws(dir: 'ws')
        echo 'test'
      }
    }

  }
}