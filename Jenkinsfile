pipeline {
  agent {
    node {
      label 'func && linux'
    }
  }

  options { disableConcurrentBuilds() }

  stages {
    stage('Format') {
      steps {
        sh '''echo Format
'''
      }
      post {
        always {
            echo 'always'
        }
        failure {
            echo 'failure'
        }
      }
    }
  }
}

