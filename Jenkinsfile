pipeline {
    agent any

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
        } 
        
    }
}
