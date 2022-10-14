node {
    stage ('SCM'){
        checkout scm
    }
    
    stage('Build1') {
        git 'https://github.com/XioRojas/DOTT.git'

        def mvnHome = tool 'mvn1'
        withMaven(){
            sh "${mvnHome}/bin/mvn --batch-mode clean install"
            sh "${mvnHome}/bin/mvn --batch-mode clean compiler:compile"
        }
    }
    
    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    stage('UTest') {
        def mvnHome = tool 'mvn1'
        withMaven(){
             sh "${mvnHome}/bin/mvn --batch-mode test"
            sh "${mvnHome}/bin/mvn --batch-mode -Dmaven.test.failure.ignore=true test"
        }
    }

    stage('Package') {
        def mvnHome = tool 'mvn1'
        withMaven(){
            sh "${mvnHome}/bin/mvn --batch-mode package -DskipsTest"
        }
    }
}
