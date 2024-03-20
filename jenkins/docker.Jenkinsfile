pipeline {
    agent any

    stages {
        stage('Checkout Git') {
            steps {
                sh 'https://github.com/aesaganda/app.git .'
            }
        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        }
    }
}