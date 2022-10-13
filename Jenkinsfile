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

    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonarqube-xio';
        withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
    stage('Deploy') {
        sh "./jenkins/scripts/deliver.sh"
    }
}
