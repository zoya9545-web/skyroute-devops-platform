pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'YOUR_GITHUB_REPO'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t skyroute-app .'
            }
        }

        stage('Run Container Test') {
            steps {
                sh 'docker run -d -p 8081:80 skyroute-app'
            }
        }

    }
}
