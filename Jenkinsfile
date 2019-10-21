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
	    //commitIdtmp = sh(returnStdout: true, script: 'git show ${commitIdtmp} -s --format=\'%ae\'').trim()
            commitIdtmp = sh(returnStdout: true, script: "git show ${commitIdtmp} -s").trim()
            echo "----------------------------------4"
	    echo commitIdtmp
	    echo "----------------------------------5"
	    commitIdtmp = sh(returnStdout: true, script: "git show ${commitIdtmp} -s --format='%ae'").trim()
	    echo "----------------------------------6"
            echo commitIdtmp
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
      script {
		echo ${env.BRANCH_NAME}
        if (${env.BRANCH_NAME} == 'master') {
		  emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS',
	               body: '''${SCRIPT, template="groovy-html.template"}''',
			       recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
			       to:'marijana.leaba@googlemail.com')
		  echo ${env.BRANCH_NAME}
		}
		else if (env.BRANCH_NAME.startsWith('PR')) {
		  echo "-----------------------PR"
		  emailext(subject: '[Jenkins] $PROJECT_NAME | $BUILD_STATUS',
	               body: '''${SCRIPT, template="groovy-html.template"}''',
			       recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
			       to:getMailsFromCurrentBuild())
		  echo ${env.BRANCH_NAME}
		}
        else {
          echo "-----------------------what is this"
        }
	  }
    }
  }
}
