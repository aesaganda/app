pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aesaganda/app.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw package'
            }
        }

        stage('Run') {
            steps {
                sh 'nohup java -jar ./target/app-0.0.1-SNAPSHOT.jar &'
            }
        }
    }
}