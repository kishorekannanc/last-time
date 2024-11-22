pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('credentials')
        DOCKER_REPO = 'kishorekannan23/prod'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kishorekannanc/last-time.git'
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
        withCredentials([usernamePassword(credentialsId: 'credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
            sh '''
            echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
            docker push kishorekannan23/prod:latest
            '''
        }
    }
}
        stage('Run Docker Container') {
    steps {
        script {
            sh '''
            docker run -d -p 80:80 --name devops-react-app $DOCKER_REPO:latest
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
