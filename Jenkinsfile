pipeline {
  agent any
  stages {
  stage("test") {
  steps {
  bat 'gradlew test'
   cucumber buildStatus: 'UNSTABLE',
                  reportTitle: 'JenkinsTP',
                  fileIncludePattern: '**/*.json',
                  trendsLimit: 10,
                  classifications: [
                      [
                          'key': 'Browser',
                          'value': 'Firefox'
                      ]
                  ]
  }

  }

}

}