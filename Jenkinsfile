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

  post {
    always {
        sh '''echo always'''
    }
    success {
            echo 'This will run only if successful'
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
    }
    failure {
            echo 'This will run only if failed'
    }
    unstable {
            echo 'This will run only if the run was marked as unstable'
    }
    changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
    }
  }
}

