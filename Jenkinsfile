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
               echo "mvn test -Dtags='type:ApiTests'"
            }
        }
        stage('Archive Reports') {
          parallel {
            stage('API Cucumber Results') {
              steps {
                archiveArtifacts(artifacts: 'target/api-cucumber-reports/', allowEmptyArchive: true)
              }
            }
          }
        }
        stage('UI Test') {
            steps {
               echo "mvn test -Dtags='type:FeatureAutomationTest'"
            }
        }
    }
}