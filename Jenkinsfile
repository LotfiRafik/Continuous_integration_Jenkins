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
        mail(subject: 'TP8', body: "${message}", to: 'gl_bouchafa@esi.dz', cc: 'gn_bouraba@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              sh '/opt/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'
            }

            waitForQualityGate true
          }
        }
        

        stage('Test Reporting') {
          steps {
            jacoco(execPattern: 'build/jacoco/*.exec', exclusionPattern: '**/test/*.class')
          }
        }

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

    stage('Slack Notification') {
      when {
        branch 'master'
      }
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', token: 'TREJHRA8Z/BT5SZUNJ3/5kR7yh20MxsyT6bjMmBye8v8', teamDomain: 'outils', channel: 'jenkins', message: 'Deployment maven TP8  Done')
      }
    }

  }
}