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
  }
  }


  








