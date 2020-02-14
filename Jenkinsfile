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
        stage('API Test Reports') {
            steps {
                archiveArtifacts(artifacts: 'target/api-cucumber-reports/', allowEmptyArchive: true)
            }
        }
        stage('UI Test') {
            steps {
               echo "mvn test -Dtags='type:FeatureAutomationTest'"
            }
        }
    }
}