pipeline {
    agent any
    tools {
        maven 'Maven 3.6.3'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kranthi619/star-agile-project-demo-dummy.git'
            }
        }
        stage('Build') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Test') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh 'mvn test'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'systemctl stop tomcat9'
                sh 'rm -rf /var/lib/tomcat9/webapps/*'
                sh 'cp target/*.war /var/lib/tomcat9/webapps/'
                sh 'systemctl start tomcat9'
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
