string setBuildEmail() {
    TMP_GIT_COMMITTER_EMAIL = sh(
      script: "git --no-pager show -s --format='%ae'",
      returnStdout: true
    ).trim()
    return $TMP_GIT_COMMITTER_EMAIL
}

pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage('build') {
      steps {
        sh "/bin/echo"
        setBuildEmail();
      }
    }
  }
  post {
    always {
      emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS', 
               body: '''${SCRIPT, template="groovy-html.template"}''', 
               recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
               to:'marijana.leaba@gmail.com'
               )
    }
  }
}
