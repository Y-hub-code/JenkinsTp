pipeline {
  agent any
  stages {
  stage("test") {
  steps {
  bat 'gradlew test'
  bat 'gradlew check'
  }

  }

}
post {
        always {
            junit 'build/reports/**/*.xml'
        }
    }
}

}