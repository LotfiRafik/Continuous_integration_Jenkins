


def message =""
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
      post 
      {
        always { script { message = "Binome : Bouchafa Lotfi , Bouraba Nazih , \n Build compeleted" } }
        failure { script { message += "Build failed" } }
        success { script { message += "Build sucess" } }
        }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'TP8', body: "${message}", to: 'h_mokeddem@esi.dz',cc:'gl_bouchafa@esi.dz')
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
