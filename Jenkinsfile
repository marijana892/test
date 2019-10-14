
def getEmail() {
    def m = env.GIT_AUTHOR_EMAIL
    if (m) {
        echo 'first if'
        def result = sh(
            script: """#!/bin/bash
            git --no-pager show -s --format='%ae'
            """,
            returnStdout: true).trim();
        echo result
        return result.trim()
    } else {
        echo 'first else'
        echo "${env.GIT_AUTHOR_EMAIL}"
        return env.GIT_AUTHOR_EMAIL
    }
}

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
          getEmail();
      }
    }
  }
  post {
        always {
            echo 'I will always say Hello again!'

            //emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS', 
              //       body: '''${SCRIPT, template="groovy-html.template"}''', 
                //     recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
                  //   to:'$CHANGE_AUTHOR_EMAIL')

            
        }
    }
}
