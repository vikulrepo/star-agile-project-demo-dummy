pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your/repo.git'
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
        stage('Deploy') {
            steps {
                sh 'sudo systemctl stop tomcat9'
                sh 'sudo rm -rf /var/lib/tomcat9/webapps/*'
                sh 'sudo cp target/*.war /var/lib/tomcat9/webapps/'
                sh 'sudo systemctl start tomcat9'
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
