pipeline {
  agent any
  stages {
  stage("test") {
  steps {
 bat 'gradlew test'
  junit 'build/test-result/test/binary/.xml'

  }

  }






}
}