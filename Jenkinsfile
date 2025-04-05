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
                withDockerRegistry(usernamePassword[credentialsId: 'docker-hub-credentials', username: '$Docker_User',Password: '$Docker_Pass']) {
                    sh 'docker login -u $Docker_User -p $Docker_Pass'
                    sh 'docker push $Docker_User/$DOCKER_IMAGE'
                }
            }
        }
    }
}


