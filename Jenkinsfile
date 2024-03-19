pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }

    environment{
        registry = "aesaganda/jenkins-docker"
        registryCredential = 'dockerhub'        
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Run') {
            steps {
                sh 'nohup java -jar ./target/app-0.0.1-SNAPSHOT.jar &'
            }
        }

        stage('Building image') {
          steps{
            script {
              dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
          }
        }
        
        stage('Deploy Image') {
          steps{
            script {
              docker.withRegistry( '', registryCredential ) {
                dockerImage.push()
              }
            }
          }
        }
}
