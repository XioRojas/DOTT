node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube-xio';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
  
  tools {maven "mvn1"}
  
  stage('Example') {
    steps {
        sh 'mvn config ls'
      }
    }
}
