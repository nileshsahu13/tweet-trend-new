pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment {
        PATH="/opt/apache-maven-3.9.9/bin:$PATH"
    }

    stages {
        stage("build"){
            steps{

                sh 'mvn clean install -U'
            }

        }
        stage('SonarQube analysis') {
                environment{
                    scannerHome = tool 'nilesh-sonar-scanner'
                }
                steps{  
                withSonarQubeEnv('nilesh-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                }
                }
        }
    }
}
