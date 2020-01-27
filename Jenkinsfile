

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle test'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*.*'
        archiveArtifacts 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'TP8', body: 'gradle build completed', to: 'gl_bouchafa@esi.dz')
      }
    }

    stage('Code Analysis') {
      steps {
        waitForQualityGate true
        withSonarQubeEnv 'TP8'
      }
    }

  }
}
