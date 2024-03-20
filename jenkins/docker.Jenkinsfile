pipeline { 

    environment { 
        registry = "aesaganda/jenkins-docker" 
        registryCredential = 'jenkinsCredentialId' // Use Jenkins credential ID
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
                    docker.withRegistry('https://your.docker.registry', registryCredential ) { 
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