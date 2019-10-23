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
	  echo "1---->abortPreviousBuilds"
          sleep(time:3,unit:"SECONDS")
          echo "2---->abortPreviousBuilds"
          abortPreviousBuilds()
          echo "3---->abortPreviousBuilds"
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
