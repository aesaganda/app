pipeline { 

    environment { 
        registry = "aesaganda/jenkins-docker" 
        registryCredential = '6c49e5ac-fce3-4b50-a936-90e0b03fddd3' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/aesaganda/app.git' 
            }
        } 
        stage('Building our image') { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy our image') { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
        stage('Cleaning up') { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
}
