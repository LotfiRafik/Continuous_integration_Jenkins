pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle test'
        archiveArtifacts 'build/libs/*.jar'
        junit 'build/test-results'
        archiveArtifacts 'build/docs/javadoc'
      }
    }

  }
}