import hudson.model.Result
import hudson.model.Run
import jenkins.model.CauseOfInterruption.UserInterruption

def abortPreviousBuilds() {
    Run previousBuild = currentBuild.rawBuild.getPreviousBuildInProgress()

    while (previousBuild != null) {
        if (previousBuild.isInProgress()) {
            def executor = previousBuild.getExecutor()
            if (executor != null) {
                echo ">> Aborting older build #${previousBuild.number}"
                executor.interrupt(Result.ABORTED, new UserInterruption(
                    "Aborted by newer build #${currentBuild.number}"
                ))
            }
        }

        previousBuild = previousBuild.getPreviousBuildInProgress()
    }
}

pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage('build') {
      steps {
          sleep(time:3,unit:"SECONDS")
          echo "B---->getMailsFromCurrentBuild"
          getMailsFromCurrentBuild()
          echo "E---->getMailsFromCurrentBuild"
      }
    }
	  
	  
  }
    post {
    always {
      script {
	      echo "${env.BRANCH_NAME}"
      }
    }
  }
}
