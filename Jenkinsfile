pipeline {
    agent any
    stages {
        stage ("Build Backend") {
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ("Unit Tests") {
            steps {
                bat 'mvn test'
            }
        }
        stage ('Deploy backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'Tomcat', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }

    }
}