pipeline{
    node("node1")
    environment{
        DOCKER_REGISTRY = "subhanshu0027"
        IMAGE_NAME = "my_react_app"
        DOCKER_CREDENTIALS_ID = "Docker_Cred"
        APP_PORT = "3000"
    }
    stages{
        stage('Clone repository'){
            steps{
                checkout scm
            }
        }

        stage("Build and push docker image"){
            steps{
                script{
                    def imageTag = "${DOCKER_REGISTRY}/${IMAGE_NAME}:latest"

                    // Build Docker image
                    def builtImage = docker.build(imageTag)

                    // Log in to Docker Hub and push
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_CREDENTIALS_ID) {
                        builtImage.push() }
                        
                }
            }

        }

        stage("Deploy to server"){
            steps{
                sh '''
                    sshpass -p 'Aes@101$' ssh aes@10.27.27.16 << EOF
                            set +x
                            export DOCKER_USERNAME=\$(docker-credential-jenkins get ${DOCKER_REGISTRY} | jq -r '.Username')
                            export DOCKER_PASSWORD=\$(docker-credential-jenkins get ${DOCKER_REGISTRY} | jq -r '.Secret')
                            docker login -u \$DOCKER_USERNAME -p \$DOCKER_PASSWORD
                            docker pull ${DOCKER_REGISTRY}/${IMAGE_NAME}:latest
                            docker run -d -p 3000:3000 ${DOCKER_REGISTRY}/${IMAGE_NAME}:latest
                        << EOF
                    '''
            }

        }
    }

}
            
