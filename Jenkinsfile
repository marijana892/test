

void setBuildEmail() {
    
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
            def myVariable = sh script: "git --no-pager show -s --format='%ae'", returnStatus: true
            echo 'I will always say Hello again!'
            echo "${myVariable}"
            
            def TMP_GIT_COMMITTER_EMAIL = sh(
      script: "git --no-pager show -s --format='%ae'",
      returnStdout: true
    ).trim()
            echo TMP_GIT_COMMITTER_EMAIL
            //echo '${CHANGE_AUTHOR_EMAIL}'
            //emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS', 
              //       body: '''${SCRIPT, template="groovy-html.template"}''', 
                //     recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
                  //   to:'$CHANGE_AUTHOR_EMAIL')

            
        }
    }
}
