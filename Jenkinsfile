pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
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

    post {
        always {
            sh 'curl http://localhost:9001/api/foos?val=TEST'
        }
        failure {
            mail to: 'team@example.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}