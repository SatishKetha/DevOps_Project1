// def registry = 'https://valaxy05.jfrog.io'
pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}

    stages {
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy'
                 echo "----------- build completed ----------"
            }
        }

        stage("SonarQube analysis") {
            environment {
            scannerHome = tool 'satish-sonarqube-scanner'
            }
            steps {
            withSonarQubeEnv('satish-sonarqube-scanner') { // If you have configured more than one global server connection, you can specify its name
            sh "${scannerHome}/bin/sonar-scanner"
            }
            }
        }     
    }

    
}