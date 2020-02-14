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
          stage('API Test') {
            steps {
              withMaven(maven: 'maven_3_6_0') {
                echo 'mvn test -Dcucumber.options="--tags @ApiTests"'
              }
            }
          }
          stage('Archive') {
               parallel {
                 stage('Cucumber Results') {
                   steps {
                     archiveArtifacts(artifacts: 'target/api-cucumber-reports/', allowEmptyArchive: true)
                   }
                 }
               }
             }
          stage('Publish') {
            parallel {
              stage('Cucumber Report') {
                steps {
                  cucumber(fileIncludePattern: '**/*.json', fileExcludePattern: '**/*usage.json', jsonReportDirectory: 'target/api-cucumber-reports/json/', sortingMethod: 'ALPHABETICAL')
                }
              }
              stage('Quality Chart') {
                steps {
                  publishHTML(allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportDir: 'target/api-cucumber-reports/html/', reportFiles: 'API-Test-overview-chart.html', reportName: 'API Test Report')
                }
              }
            }
          }
      }
}