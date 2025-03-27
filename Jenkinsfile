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
                sh 'mvn clean package -Dmaven.test.skip=true'  // ✅ Ensures target/classes exists
            }
        }

        stage("SonarQube analysis") {
            environment {
                scannerHome = tool 'nilesh-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('nilesh-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner "  // ✅ Explicitly specify the path
                }
            }
        }
    }
}
