
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

void setBuildStatus(String context, String message, String state) {
    withCredentials([string(credentialsId: credentials('marvin-git-status-token'), variable: 'TOKEN')]) {
        def url = "https://github.com/marijana892/test/statuses/" + getCommitHash().trim() +
            "?access_token=$TOKEN"
        echo url
        sh """#!/bin/bash
        set - x
        curl \"${url}\" \
                -H \"Content-Type: application/json\" \
                -X POST \
                -d \"{\\\"description\\\": \\\"$message\\\", \\\"state\\\": \\\"$state\\\", \\\"context\\\": \\\"$context\\\", \\\"target_url\\\": \\\"$BUILD_URL\\\"}\"
        """
    }
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
          setBuildStatus()
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
