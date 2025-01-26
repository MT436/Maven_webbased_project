pipeline

agent any

// Need to set up the path for the required in manage jenkins>Tools 
tools {
  git 'Default'
  jdk 'JAVA'
  maven 'Maven'
}

// discard builds when they reach a certain age; for example, one days old; quietPeriod option allows specifying a quiet period for this project; Retry the block (up to N times) if any exception happens during its body execution
options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '1', numToKeepStr: '5')
  quietPeriod 20
  retry(3)
}

stages {
  stage("Deletes the workspace once build is done"){
    steps {
     cleanWs() 
    }
  }
  stage('Build') {
    steps {
    // One or more steps need to be included within the steps block.
      mvn clean package
    }
  }
}
