def getMailByCommitId(String commitId) {
  echo "log getMailByCommitId 1\n"
    def result = sh(
            script: """#!/bin/bash
            set - x
            git show ${commitId} -s --format='%ae'
""",
            returnStdout: true).trim();
   echo "log getMailByCommitId 2\n"
  return result;
}
def getMailsFromCurrentBuild() {
    def changes = ""
    def commitIdtmp = ""
    currentBuild.changeSets.each { set ->
        set.each { entry ->
            echo "${entry.commitId} by ${entry.author.fullName}\n"
            echo "----------------------------------1"
            commitIdtmp = "${entry.commitId}"
            echo "----------------------------------2"
            echo commitIdtmp
            echo "----------------------------------3"
            getMailByCommitId(commitIdtmp)
            echo "----------------------------------4"
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
          echo "B---->getMailsFromCurrentBuild"
          getMailsFromCurrentBuild()
          echo "E---->getMailsFromCurrentBuild"
      }
    }
	  
	  
  }
  post {
        always {
            echo 'I will always say Hello again!'
        }
    }
}
