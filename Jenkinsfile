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
        
        stage('Docker Login') { 
            steps { 
                withCredentials([usernamePassword( credentialsId: 'Dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS' )]) {
                    sh """
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE:latest
                    """
                } 
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
