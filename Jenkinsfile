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
                withMaven(maven: 'maven_3_2') {
                    echo "mvn clean verify -Dtags='type:ApiTests'"
                }
            }
        }
    }
}