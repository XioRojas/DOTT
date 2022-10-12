node {
    stage('Build') {
        checkout scm
    }
    stage ('SonarQube Analysis') {
        scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
}
