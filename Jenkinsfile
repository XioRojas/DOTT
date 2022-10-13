node {
    stage ('SCM'){
        checkout scm
    }
    
    stage('Build') {
        git 'https://github.com/XioRojas/DOTT.git'

        def mvnHome = tool 'mvn1'
        withMaven(){
            sh "${mvnHome}/bin/mvn clean install"
            sh "${mvnHome}/bin/mvn clean compile test"
        }
    }

    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
    stage('Example') {
        def maven = tool 'mvn1'
        sh "${mvnHome}/bin/mvn config ls"
    }
}
