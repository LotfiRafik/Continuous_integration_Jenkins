pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'sh \'gradle build\''
        sh 'sh \'gradle javadoc\''
        sh 'sh \'gradle test\''
        archiveArtifacts '\'build/libs/*.jar\''
        junit '\'build/test-results\''
        archiveArtifacts '\'build/docs/javadoc\''
      }
    }

  }
}