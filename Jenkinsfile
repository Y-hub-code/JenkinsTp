pipeline {
  agent any
  stages {
  stage("test") {
  steps {
 bat './gradlew test'
 junit 'build/test-results/**/*.xml'
   cucumber buildStatus: 'SUCCESS',
                 reportTitle: 'My report',
                 fileIncludePattern: 'target/*.json',
                 trendsLimit: 10
    
  }
  }
 stage('Code Analysis') {
    
    steps {
            withSonarQubeEnv('sonar') {
              bat './gradlew sonar'
            }
      waitForQualityGate  abortPipeline:true
 }
 }
 stage('Build') {
   
   steps {
        bat './gradlew build'
        bat './gradlew javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
     
      }
 }
    
  stage('Deploy') {
  steps {
        bat './gradlew publish'
      }
  
  
  }
    
    stage('Notification') {
      steps {
        notifyEvents message: 'build success', token: 'J7PQleEBxcVbQ2nXUywf0ODZ5ch0TnDa'
      }
    }
    
    
     stage(' deploy Mail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jy_bachikh@esi.dz' ,bcc:'jy_bachikh@esi.dz')
      }
    }
      stage('Slack Notification') {
      steps {
        slackSend(message: 'Slack vous indique que le processus est termine avec succes. ')
      }
      }
    
    
    
    
  }
  }


  








