pipeline {
  agent {
    label 'linux'
  }
  options {
    disableConcurrentBuilds()
  }
  stages {
    stage('Shared') {
      steps {
        load 'Jenkinsfile_include'
      }
    }
  }
}
