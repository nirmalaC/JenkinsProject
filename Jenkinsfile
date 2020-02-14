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
          stage('Archive') {
               parallel {
                 stage('Cucumber Results') {
                   steps {
                     archiveArtifacts(artifacts: 'output/*.txt', allowEmptyArchive: true)
                   }
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
              stage('Quality Chart') {
                steps {
                  publishHTML(allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportFiles: 'API-Test-overview-chart.html', reportName: 'API Test Report')
                }
              }
            }
          }
      }
}