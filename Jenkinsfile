pipeline {
  agent any
  stages {
  stage("test") {
  steps {
  bat 'gradlew test'
   cucumber 'reports/*json'
  }

  }

}

}