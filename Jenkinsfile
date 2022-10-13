pipeline {
    agent any
    
    tools {
        maven "mvn1"
        scannerHome 'sonarqube-xio'
    }
    
    stages {
        stage('Build') {
            steps{
                git "https://github.com/XioRojas/DOTT.git"
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }

  stage('SonarQube Analysis') {
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
