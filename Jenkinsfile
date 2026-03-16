pipeline {
    agent any

    environment {
        IMAGE = "sahilkulkarni585/devops-demo"
    }

    stages {
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }
        
        stage('Docker Push') { 
            steps { 
            sh 'docker push $IMAGE_NAME:latest' 
        }
    }
        stage('Docker Login') { 
            steps { 
                withCredentials([usernamePassword( credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS' )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin' } 
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
}
