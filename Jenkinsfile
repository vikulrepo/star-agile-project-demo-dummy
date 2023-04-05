pipeline {
    agent any
    tools {
        maven 'Maven 3.6.3'
    }
    stages {
        stage('Checkout') {
            steps {
               sh 'echo passed'
                //git branch: 'master', url:'https://github.com/kranthi619/star-agile-project-demo-dummy'
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
