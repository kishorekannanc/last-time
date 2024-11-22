pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('credentials')
        DOCKER_REPO = 'kishorekannan23/dev'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev', url: 'https://github.com/kishorekannanc/last-time.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_REPO:latest .'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    sh '''
                    echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKER_HUB_CREDENTIALS_USR --password-stdin
                    docker push $DOCKER_REPO:latest
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Build and push successful.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}

