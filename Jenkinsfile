pipeline {
  agent any
  stages {
  stage("test") {
  steps {
 bat 'gradlew test'
  }
  steps {
   bat 'gradlew check'
  }

  }

}
post {
        always {
            junit 'build/test-result/test/binary/.xml'
        }
    }
}

}