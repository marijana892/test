def myVariable = "foo"

void setBuildEmail() {
    TMP_GIT_COMMITTER_EMAIL = sh(
      script: "git --no-pager show -s --format='%ae'",
      returnStdout: true
    ).trim()
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
            echo 'I will always say Hello again!'
            echo $CHANGE_AUTHOR_EMAIL
            echo $PROJECT_NAME
            //emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS', 
            //         body: '''${SCRIPT, template="groovy-html.template"}''', 
            //         recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
            //         to:'marijana.leaba@gmail.com')

            
        }
    }
}
