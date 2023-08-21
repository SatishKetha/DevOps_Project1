// def registry = 'https://valaxy05.jfrog.io'
pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stages {
        stage ('clone-code') {
            steps {
                git branch: 'main', url: 'https://github.com/SatishKetha/DevOps_Project1.git'
            }

        }
    }
}