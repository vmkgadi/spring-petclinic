pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vmkgadi/spring-petclinic.git'
            }
        }       
    }
}
