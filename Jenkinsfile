node {
  stage('Build') {
    git https://github.com/XioRojas/DOTT.git
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube-xio';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
