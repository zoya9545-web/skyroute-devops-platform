pipeline {
agent any

```
environment {
    DOCKER_IMAGE = "zoya9545/skyroute-devops-app"
}

stages {

    stage('Clean Workspace') {
        steps {
            deleteDir()
        }
    }

    stage('Clone Repository') {
        steps {
            git branch: 'main', url: 'https://github.com/zoya9545-web/skyroute-devops-platform.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t $DOCKER_IMAGE .'
        }
    }

    stage('Push Docker Image') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }

    stage('Deploy to Kubernetes') {
        steps {
            sh 'kubectl apply -f deployment.yaml'
            sh 'kubectl apply -f service.yaml'
        }
    }

    stage('Verify Deployment') {
        steps {
            sh 'kubectl get pods'
            sh 'kubectl get svc'
        }
    }

}
```

}
