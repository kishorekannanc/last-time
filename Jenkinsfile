pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub')
        DOCKER_REPO = 'kishorekannan23/prod'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/sriram-R-krishnan/devops-build.git'
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

