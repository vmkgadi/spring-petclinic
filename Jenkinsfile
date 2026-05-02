pipeline {
    agent any
    environment {
        IMAGE_NAME = "vmkfens/tech"
        TAG = "${env.BUILD_NUMBER}
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vmkgadi/spring-petclinic.git'
            }
        } 
        stage('Package') {
            steps {
                sh 'mvn clean package '
            }
        } 
        stage('Test') {
            steps {
                sh 'mvn test '
            }
        } 
        stage('Build Docker') {
            steps {
                sh 'docker build -t vmkgadi/tech:$BUILD_NUMBER .'
            }
        } 
        stage('Push Docker Image') {
    steps {
        withDockerRegistry(credentialsId: 'dock', url: 'https://index.docker.io/v1/') {
            sh 'docker push vmkgadi/tech:$BUILD_NUMBER'
        }
    }
}
        stage('Deploy to Dev') {
            steps {
                sh '''
                docker stop petclinic-dev || true
                docker rm petclinic-dev || true
                docker run -d -p 8085:8080 --name petclinic-dev $IMAGE_NAME:$TAG
                '''
            }
        }
        stage('Approve Production') {
            steps {
                input message: "Deploy to production?"
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                docker stop petclinic-prod || true
                docker rm petclinic-prod || true
                docker run -d -p 8089:8080 --name petclinic-prod $IMAGE_NAME:$TAG
                '''
            }
        }

        }       
}
