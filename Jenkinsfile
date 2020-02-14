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
                echo "mkdir -p Output"
                writeFile file: "output/Reports.txt", text: "This file is useful, need to archive it."
                writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."
              }
            }
          }
          stage('Archive') {
               parallel {
                 stage('Cucumber Results') {
                   steps {
                     archiveArtifacts (artifacts: 'Output/*.txt', excludes: 'output/*.md')
                   }
                 }
               }
             }
          stage('Make Directory') {
                steps {
                  echo "mkdir -p CucumberReport"
                }
          }
          node {
           stage ('Record Reports')
           step([$class: 'CucumberTestReportPublisher', reportsDirectory: 'CucumberReport', fileIncludePattern: '**/*.json'])
          }
          stage('Quality Chart') {
                steps {
                  publishHTML(allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportDir: 'CucumberReport', reportFiles: 'API-Test-overview-chart.html', reportName: 'Test Report')
                }
          }
      }
}