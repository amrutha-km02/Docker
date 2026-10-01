pipeline{
    agent any

    environment{
        DOCKER_IMAGE = "amruthakm02/agoda"
    }
    stages{
        stage('clone repository'){
            steps{
                git 'https://github.com/amruthakm02/https://github.com/amrutha-km02/Docker.git'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }
        stage('login to Docker Hub'){
            steps{
                withcredentials([usernamePassword(
                    credentialsID:';dockerhub-creds',
                    usernameVariable:'DOCKER_USER',
                    passwordVariable:'DOCKER_PASS'
                )]){
                    bat 'echo $DOCKER_PASS | docker login -u $DOCKRER_USER --password-stdin'
                }
            }
        }
        stage('Push Docker Image'){
            steps{
                script{
                    docker.withRegistry('','dockerhub-creds'){
                        docker.image("${agoda}:latest").push()
                    }
                }
            }
        }
    }
    post{
        success{
            echo 'Image successfully built and pushed to Docker Hub'
        }
        failure{
            echo 'Pipeline failed'
        }
    }
}
