pipeline {
      agent any
      stages {
            stage('checkout') {
              steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nirmalaC/HotelBookingSystem.git']]])
              }
            }
          stage('Test') {
            steps {
                withMaven(jdk: 'JAVA_HOME', maven: 'maven_3_6_0') {
                     echo 'Test Started'
                     powershell label: '', script: 'mvn test'
                     echo 'Test Finished'
                }
            }
          }
          stage('Make Directory') {
                steps {
                  powershell label: '', script: 'mkdir -p CucumberReport'
                }
          }
          stage('Cucumber Reports'){
            steps{
                cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
            }
          }
          stage('Quality Chart') {
                steps {
                  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'CucumberReport', reportFiles: 'index.html', reportName: 'CucumberReport', reportTitles: ''])

               }
          }
      }
}