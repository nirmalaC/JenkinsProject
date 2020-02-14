pipeline {
      agent any
      stages {
            stage('checkout') {
              steps {
                git branch: 'master',
                  url: 'https://github.com/nirmalaC/HotelBookingSystem.git'
                echo 'mvn clean install -DskipTests=true'
              }
            }
          stage('Test') {
            steps {
              withMaven(maven: 'maven_3_6_0') {
                echo 'mvn test'
              }
            }
          }
          stage('Publish') {
            parallel {
              stage('Cucumber Report') {
                steps {
                  cucumber(fileIncludePattern: '**/*.json', fileExcludePattern: '**/*usage.json', sortingMethod: 'ALPHABETICAL')
                }
              }
            }
          }
      }
}