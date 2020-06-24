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
        stage ('Deploy frontend') {
            steps {
                dir('frontend'){
                    git 'https://github.com/gerafenster/tasks-frontend'
                    bat 'mvn clean package'              
                    deploy adapters: [tomcat8(credentialsId: 'Tomcat', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks', war: 'target/tasks.war'
                }
            }
        }

    }
}