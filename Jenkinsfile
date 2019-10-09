void setBuildEmail() {
    TMP_GIT_COMMITTER_EMAIL = sh(
      script: "git --no-pager show -s --format='%ae'",
      returnStdout: true
    ).trim()
    echo "TMP_GIT_COMMITTER_EMAIL: $TMP_GIT_COMMITTER_EMAIL"
}

pipeline {
  agent {
    label 'whatever'
  }
  stages {
    stage('build') {
      steps {
        sh "/bin/echo"
      }
    }
    stage('test in docker') {
      agent {
        docker {
          image 'ubuntu:18.04'
          reuseNode true
        }
      }
      steps {
        sh "/bin/echo"
      }
    }
  }
}
