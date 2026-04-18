pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git url: 'https://github.com/rapoluvinaykumar94-hub/java-devops-project.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests || mvn clean package -DskipTests'
            }
        }

        stage('Docker Clean') {
            steps {
                sh 'docker rm -f java-app || exit 0'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t java-app .'
            }
        }

       stage('Docker Run') {
           steps {
               sh 'docker rm -f java-app || true'
               sh 'docker run -d -p 9091:8080 --name java-app java-app'
           }
       }
          
       stage('Deploy to Kubernetes') {
         steps {
             sh '''
              export KUBECONFIG=/var/lib/jenkins/config
              kubectl apply -f deployment.yml
              kubectl apply -f service.yml
              '''
          }
       }
    }
}
