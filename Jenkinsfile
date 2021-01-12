pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk9'
    }
    parameters {
        booleanParam(name: "Performrelease ?", description : '', defaultValue: false)
    }
    stages {
        stage('Initialize') {
            steps {
                sh '''
                    echo "PATH ${PATH}"
                    echo "M2_HOME ${M2_HOME}"
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'SonarScanner4'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}