def getMailByCommitId(String commitId) {
    def result = sh(
            script: """#!/bin/bash
            set - x
            git show ${commitId} -s --format='%ae'
""",
            returnStdout: true).trim();
        return result.trim()
}

def changelist() {
    def changes = ""
    currentBuild.changeSets.each { set ->
        set.each { entry ->
            echo "${entry.commitId} by ${entry.author.fullName}\n"
			changes += getMailByCommitId(entry.commitId)
			changes += " "
        }
    }
    return changes
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
