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
           sh "mvn clean verify -Dtags='type:ApiTests'"

           finally {
               publishHTML (target: [
               reportDir: 'target/api-cucumber-reports/',
               reportFiles: 'index.html',
               reportName: "API tests report"
               ])
           }
        }
        stage('UI Test') {
            steps {
                sh 'mvn test -Dcucumber.options="--tags @FeatureAutomationTest"'
            }
        }
        stage('UI Test Reports') {
            steps {
                archiveArtifacts(artifacts: 'target/ui-cucumber-reports/', allowEmptyArchive: true)
            }
        }
    }
}