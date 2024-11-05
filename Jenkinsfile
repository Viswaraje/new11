pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Viswaraje/new11.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build("viswaraje/nodejs-api:elevenpart")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials-id') {
                        docker.image("viswaraje/nodejs-api:elevenpart").push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Remove existing container if it exists
                    sh 'docker rm -f nodejs-api || true'
                    // Run Docker container
                    sh 'docker run -d --name nodejs-api -p 3001:3000 viswaraje/nodejs-api:elevenpart'
                }
            }
        }
    }
}
