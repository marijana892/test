def myVariable = "foo"
def TMP_GIT_COMMITTER_EMAIL;

void setBuildEmail() {
    myVariable = sh script: "git --no-pager show -s --format='%ae'", returnStatus: true
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
            echo myVariable
            echo TMP_GIT_COMMITTER_EMAIL
            //echo '${CHANGE_AUTHOR_EMAIL}'
            //emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS', 
              //       body: '''${SCRIPT, template="groovy-html.template"}''', 
                //     recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
                  //   to:'$CHANGE_AUTHOR_EMAIL')

            
        }
    }
}
