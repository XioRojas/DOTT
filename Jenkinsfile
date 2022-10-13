node {
    stage ('SCM'){
        checkout scm
    }
    
    stage('Test') {
        git 'https://github.com/XioRojas/DOTT.git'
        
        def mvnHome = tool 'mvn1'
        withMaven(){
            sh "${mvnHome}/bin/mvn --batch-mode -Dmaven.test.failure.ignore=true test"
        }
    }

        stage('Package') {
        def mvnHome = tool 'mvn1'
        withMaven(){
            sh "${mvnHome}/bin/mvn --batch-mode package -DskipsTest"
        }
    }
    
    
    post {
        always {
            archiveArtifacts artifacts: "build/libs/**/*.jar", fingerprint: true
            junit "build/reports/**/*.xml", allowEmptyResults: true
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
