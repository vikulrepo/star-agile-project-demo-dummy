pipeline {
    agent any
    tools {
        maven 'Maven 3.6.3'
    }
    stages {
        stage('Checkout') {
            steps {
               checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Verify') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    retry(5) {
                        sh 'curl http://localhost:8080/app'
                    }
                }
            }
        }
    }
}
