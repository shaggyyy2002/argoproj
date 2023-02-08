pipeline{

    agent any 

    environment{
        DOCKERHUB_USERNAME = 'nitin03'
        APP_NAME = "argoproj"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = "dockerhub"
    }

    stages{
        stage('Clean Workspace..'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout Github..'){
            steps{
                git branch: 'main', 
                credentialsId: 'github', 
                url: 'https://github.com/shaggyyy2002/argoproj.git'
            }
        }
        stage('Build Image..'){
            steps{
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage('Push Image to DockerHub..'){
            steps{
                script{
                    docker.withRegistry('',REGISTRY_CREDS){
                        docker_image.push('$BUILD_NUMBER')
                        docker_image.push('latest')
                }
                }
            }
        }

    }
}