pipeline {
    agent any

    environment {
        IMAGE = "sahilkulkarni585/devops-demo"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/sahilk-2002/devops-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
