pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Run App') {
            steps {
                sh 'java -jar target/*.jar --server.port=80'
            }
        }

    }
}
