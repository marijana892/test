import hudson.model.Result
import hudson.model.Run
import jenkins.model.CauseOfInterruption.UserInterruption

def abortPreviousBuilds() {
echo "abortPreviousBuilds -------------------0"
    Run previousBuild = currentBuild.rawBuild.getPreviousBuildInProgress()
echo "abortPreviousBuilds -------------------1"
    while (previousBuild != null) {
    echo "abortPreviousBuilds-------------------while---2"
        if (previousBuild.isInProgress()) {
        echo "abortPreviousBuilds-------------------if---3"
            def executor = previousBuild.getExecutor()
            if (executor != null) {
            echo "abortPreviousBuilds -------------------if---4"
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
          //sleep(time:3,unit:"SECONDS")
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
