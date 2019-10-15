
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

@NonCPS  // Necessary to allow .each to work.
def changelist() {
    def changes = ""
    currentBuild.changeSets.each { set ->
        set.each { entry ->
            //changes += "${entry.commitId} by ${entry.author.fullName}\n"
			def result = sh(script: """#!/bin/bash
                                       git show ${entry.commitId} -s --format='%ae'""",
                            returnStdout: true).trim();
			changes += result
        }
    }
	echo changes
    changes
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
          
          echo "B---->changelist"
          changelist()
          echo "E---->changelist"
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
