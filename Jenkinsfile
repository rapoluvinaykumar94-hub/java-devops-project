pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vinayreddyra/java-app"
    }

    stages {

        stage('Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/rapoluvinaykumar94-hub/java-devops-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                     echo "$PASS" | docker login -u "$USER" --password-stdin
                     docker push $DOCKER_IMAGE
                     '''
                }
            }
        }

          stage('Deploy to EKS') {
            steps {
               withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                  sh '''
                  export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                  export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                  aws eks update-kubeconfig --region us-east-1 --name <your-cluster-name>

                  kubectl get nodes
                  kubectl apply -f deployment.yml
                  kubectl apply -f service.yml
                  '''
               }
            }
        }
    }
}
