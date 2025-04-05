pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'vinayz7/my-flask-app:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url:'https://github.com/vinayz7/python_dockerfile',branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: '$DOCKER_USER',passwordVariable: '$DOCKER_PASS')]) {
                    sh 'docker login -u "$DOCKER_USER" -p "$DOCKER_PASS"'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }

        stage('Expose Service') {
            steps {
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}


