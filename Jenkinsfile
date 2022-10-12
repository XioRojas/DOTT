pipeline {
    agent any

    tools {
        maven "mvn1"
    }

    stages {
        stage ('Build') {
            steps {
                git "https://github.com/XioRojas/DOTT.git"

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }

        post {
            success {
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }

        stage ('SonarQube Analysis') {
             def scannerHome = tool 'sonarqube-xio';
             withSonarQubeEnv() {
                sh "${scannerHome}/bin/sonar-scanner"
             }
        }  
    }
}
