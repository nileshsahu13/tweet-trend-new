pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
    }
    stages {
        stage("build") {
            steps {
                sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }

        stage("SonarQube analysis") {  // ✅ Now inside 'stages'
            environment {
                scannerHome = tool 'nilesh-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('nilesh-sonarqube-server') { 
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
