void setBuildStatus(String context, String message, String state) {
}


pipeline {
  agent {
    none {
      //label 'func && linux'
    }
  }

  options { disableConcurrentBuilds() }

  stages {
    stage('Format') {
      steps {
        sh '''echo Format'''
      }
      post {
        always {
            echo 'always'
            setBuildStatus("Format", "Passed Format", "success");
        }
        failure {
            echo 'failure'
            setBuildStatus("Format", "Failure Format", "failure");
        }
      }
    }
  }
}

