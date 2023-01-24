pipeline {
  agent any
  stages {
  stage("test") {
      post {
        failure {
          script {
            mail= " test termine avec echec "
          }

        }

        success {
          script {
            mail=" test termine avec succes "
          }

        }

      }
  steps {
 bat './gradlew test'
 junit 'build/test-results/**/*.xml'
   cucumber buildStatus: 'SUCCESS',
                 reportTitle: 'My report',
                 fileIncludePattern: 'target/*.json',
                 trendsLimit: 10
    
  }
  }
     stage('EMail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jy_bachikh@esi.dz' ,bcc:'jy_bachikh@esi.dz')
      }
    }
 stage('Code Analysis') {
     post {
        failure {
          script {
            mail= " Code Analysis termine avec echec "
          }

        }

        success {
          script {
            mail=" Code analysis termine avec succes "
          }

        }

      }
    
    steps {
            withSonarQubeEnv('sonar') {
              bat './gradlew sonar'
            }
      waitForQualityGate  abortPipeline:true
 }
 }
     stage(' EMail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jy_bachikh@esi.dz' ,bcc:'jy_bachikh@esi.dz')
      }
    }
 stage('Build') {
     post {
        failure {
          script {
            mail= " Build termine avec echec "
          }

        }

        success {
          script {
            mail=" Build termine avec succes "
          }

        }

      }
   
   steps {
        bat './gradlew build'
        bat './gradlew javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
     
      }
 }
     stage('EMail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jy_bachikh@esi.dz' ,bcc:'jy_bachikh@esi.dz')
      }
    }
    
  stage('Deploy') {
       post {
        failure {
          script {
            mail= " Deployement terminé avec échec "
          }

        }

        success {
          script {
            mail=" Deployement termine avec succes "
          }

        }

      }
  steps {
        bat './gradlew publish'
      }
  
  
  }
     stage(' EMail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jy_bachikh@esi.dz' ,bcc:'jy_bachikh@esi.dz')
      }
    }
    stage(' Signal Notification') {
      steps {
        notifyEvents message: 'build success', token: 'J7PQleEBxcVbQ2nXUywf0ODZ5ch0TnDa'
      }
    }
    
      stage('Slack Notification') {
      steps {
        slackSend(message: 'Slack vous indique que le processus est termine avec succes. ')
      }
      }
    
    
    
    
  }
  }


  








