pipeline {
   agent any // Ensure 'any' is correctly spelled and placed inside the 'agent' block

// Need to set up the path for the required in manage jenkins>Tools 
tools {
  git 'Default'
  jdk 'JAVA'
  maven 'Maven'
}

// discard builds when they reach a certain age; for example, one days old; quietPeriod option allows specifying a quiet period for this project; Retry the block (up to N times) if any exception happens during its body execution
options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '1', numToKeepStr: '5')
}

stages {
  stage('Clean'){  //Deletes the workspace once build is done
    steps {
     cleanWs() 
    }
  }
  
  stage('Checkout') {  //git checkout
    steps {
      checkout scmGit(branches: [[name: '*/Pipeline']], 
                      extensions: [], 
                      userRemoteConfigs: [[url: 'https://github.com/MT436/Maven_webbased_project.git']])
    }
  }
  
  stage('Build') {
    steps {
    // One or more steps need to be included within the steps block.
      sh 'mvn clean package'
    }
  }
   stage('Test') {
    steps {
    // One or more steps need to be included within the steps block.
      sh 'mvn test'
    }
  }
   stage('sonar') {
    steps {
    // One or more steps need to be included within the steps block.
      sh 'mvn sonar:sonar'
    }
  }
   
}
}
