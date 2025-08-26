pipeline {
    environment {
        DOCKER_CONFIG = "${env.WORKSPACE}/.docker"
    }
    agent {
        docker {
            image 'docker:20.10.7'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SetsiriAunsiam/jenkins-docker-demo-app.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'mkdir -p $DOCKER_CONFIG'
                sh 'docker build -t jenkins-demo-app:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8081:8081 --name demo-app jenkins-demo-app:latest'
            }
        }
    }
}
