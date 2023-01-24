pipeline {
  agent any
  
  stages {
  stage("test") {
      post {
        failure {
          script {
            mail= " test Failed "
            
          }

        }

        success {
          script {
            mail=" test Successful "
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
     stage('EMail Test Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'etisalatte1421@gmail.com' ,bcc:'etisalatte1421@gmail.com')
      }
    }
 stage('Code Analysis') {
     post {
        failure {
          script {
            mail= " Code Analysis Failed "
          }

        }

        success {
          script {
            mail=" Code analysis Successful "
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
     stage(' EMail Code Analysis Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'etisalatte1421@gmail.com' ,bcc:'etisalatte1421@gmail.com')
      }
    }
 stage('Build') {
     post {
        failure {
          script {
            mail= " Build Failed "
          }

        }

        success {
          script {
            mail=" Build Successful "
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
     stage('EMail Build Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'etisalatte1421@gmail.com' ,bcc:'etisalatte1421@gmail.com')
      }
    }
    
  stage('Deploy') {
       post {
        failure {
          script {
            mail= " Deployement Failed "
          }

        }

        success {
          script {
            mail=" Deployement Successful "
          }

        }

      }
  steps {
        bat './gradlew publish'
      }
  
  
  }
     stage(' EMail Deploy Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'etisalatte1421@gmail.com' ,bcc:'etisalatte1421@gmail.com')
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


  








