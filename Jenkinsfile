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

    stage('Mail Notification') {
      steps {
        mail(subject: 'TP8', body: "${message}", to: 'gl_bouchafa@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              sh '/home/rafix/Desktop/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'
            }

            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            jacoco()
          }
        }

      }
    }

  }
}