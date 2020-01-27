pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'sh \'gradle build\''
        archiveArtifacts '\'build/libs/*.jar\''
      }
    }

  }
}