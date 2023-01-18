pipeline {
  agent any
  stages {
  stage("test") {
  steps {
 bat 'gradlew test'
 bat junit 'build/test-results/test/binary/TEST-Matrix.xml'

  }

  }






}
}