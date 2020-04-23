pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        always {
          script {
            message = "Binome : Bouchafa Lotfi , Bouraba Nazih , \n Build compeleted"
          }

        }

        failure {
          script {
            message += "Build failed"
          }

        }

        success {
          script {
            message += "Build sucess"
          }

        }

      }
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle test'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*.*'
        archiveArtifacts 'build/test-results/test/*.xml'
      }
    }

    stage('Unit Testing') {
      steps {
        mail(subject: 'TP8', body: "${message}", to: 'gl_bouchafa@esi.dz', cc: 'gn_bouraba@esi.dz')
      }
    }

    stage('Deployment') {
      when {
        branch 'master'
      }
      steps {
        sh 'gradle publish'
      }
    }

  }
}