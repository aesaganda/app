pipeline { 

    environment { 
        registry = "aesaganda/jenkins-docker" 
        registryCredential = '6c49e5ac-fce3-4b50-a936-90e0b03fddd3' // Use Jenkins credential ID
    }
    agent any 
    stages { 
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/aesaganda/app.git' 
            }
        } 
        stage('Building our image') { 
            steps {
                script { 
                    def dockerImage = docker.build "${registry}:${env.BUILD_NUMBER}" 
                }
            }
        } 
        
        stage('Deploy our image') { 
            steps {
                script {
                    docker.withRegistry('https://docker.io', registryCredential ) { 
                        dockerImage.push() 
                    }
                }
            }
        } 
        stage('Cleaning up') { 
            steps {
                sh "docker rmi ${registry}:${env.BUILD_NUMBER}" 
            }
        }
    }
}