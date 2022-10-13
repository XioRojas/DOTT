node {
    stage ('SCM'){
        checkout scm
    }
    
    stage('Test') {
        def mvnHome = tool 'mvn1'
        sh 'mvn clean compile test'
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }
    
    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
    
    stage('Example') {
        sh 'mvn config ls'
    }
}
