pipeline{

    agent any 

    env{
        DOCKERHUB_USERNAME = 'nitin03'
        APP_NAME = "argoproj"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = "dockerhub"
    }

    stages{
        stage('Clean Workspace..'){
            script{
                cleanWs()
            }
        }
        stage('Checkout Github..'){
            script{
                credentialsId = 'github'
                url = 'https://github.com/shaggyyy2002/argoproj.git'
                branch = 'main'
            }
        }
        stage('Build Image..'){
            script{
                docker_image = docker.build "${IMAGE_NAME}"
            }
        }
        stage('Push Image to DockerHub..'){
            script{
                docker.withRegistry('',REGISTRY_CREDS){
                    docker_image.push('$BUILD_NUMBER')
                    docker_image.push('latest')
                }
            }
        }

    }
}