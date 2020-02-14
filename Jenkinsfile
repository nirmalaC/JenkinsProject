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
              echo "mvn clean verify -Dtags='type:ApiTests'"
            }
          }
        }
        stage() {
          post {
            failure {
              echo "Test failed"
              cucumber buildStatus: 'FAIL',
                failedFeaturesNumber: 1,
                failedScenariosNumber: 1,
                skippedStepsNumber: 1,
                failedStepsNumber: 1,
                fileIncludePattern: '**/*.json',
                sortingMethod: 'ALPHABETICAL'
            }
            success {
              echo "Test succeeded"
              cucumber buildStatus: 'SUCCESS',
                failedFeaturesNumber: 0,
                failedScenariosNumber: 0,
                skippedStepsNumber: 0,
                failedStepsNumber: 0,
                fileIncludePattern: "**/cucumber.json",
                sortingMethod: 'ALPHABETICAL'

            }

          }

        }
      }
    }
}