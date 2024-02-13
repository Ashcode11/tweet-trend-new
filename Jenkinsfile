pipeline {
    agent {
        node {
            label 'Maven-Slave'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages {
        stage("Build") {
            steps {
                script {
                    echo "----------- Build started ----------"
                    sh 'mvn clean deploy -Dmaven.test.skip=true'
                    echo "----------- Build completed ----------"
                }
            }
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'ash-sonar-scanner'
            }
            steps {
                script {
                    withSonarQubeEnv('ash-sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}

