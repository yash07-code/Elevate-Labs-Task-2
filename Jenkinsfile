pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "your-dockerhub-username/flask-app"
        DOCKER_HUB_CREDENTIALS = 'dockerhub-creds'   // Jenkins credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-flask-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_HUB_REPO:latest .'
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "$DOCKER_HUB_CREDENTIALS",
                                                     usernameVariable: 'DOCKER_USER',
                                                     passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    }
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push $DOCKER_HUB_REPO:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-container $DOCKER_HUB_REPO:latest'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        failure {
            echo 'Pipeline failed'
        }
        success {
            echo 'Pipeline executed successfully '
        }
    }
}
