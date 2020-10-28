pipeline {
    agent any
    tools {
        maven 'apache-maven-3.6.3'
        jdk 'jdk8'
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
    }
}