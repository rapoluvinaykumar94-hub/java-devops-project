pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/rapoluvinaykumar94-hub/java-devops-project.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t java-app .'
            }
        }

        stage('Docker Run') {
            steps {
                bat 'docker run -d -p 9091:8080 java-app'
            }
        }

    }
}
