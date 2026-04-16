pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/rapoluvinaykumar94-hub/java-devops-project.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
    }
}
