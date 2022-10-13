node {
    stage ('SCM'){
        checkout scm
    }
    
    stage('Build') {
        sh './gradlew build'
    }
    
    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
    stage('Test') {
        sh './gradlew check'
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }
    
    stage('Example') {
        def maven = tool 'mvn1'
        sh 'mvn config ls'
    }
}
