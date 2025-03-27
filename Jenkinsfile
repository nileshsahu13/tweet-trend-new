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
                 echo "----------- build started ----------"
                sh 'mvn clean package -Dmaven.test.skip=true'  // ✅ Ensures target/classes exists
                 echo "----------- build completed ----------"
            }
        }
 #       stage("test"){
 #           steps{
    #              echo "----------- unit test started ----------"
     #           sh 'mvn surefire-report:report'
      #           echo "----------- unit test Complted ----------"
       #     }
        #}

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
