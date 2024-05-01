pipeline {
    agent any
    stages {
        stage ('git checkout') {
            steps {
                sh 'git clone https://github.com/aarkay-gummadi/Java_docker-kubernetes_project.git'

            }
        }
        stage ('Building New Docker Image') {
            steps {
                script {
                    dir('./productcatalogue') {
                        //  Building new image
                        sh 'mvn clean install'
                        sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
                        sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'
                        echo "Image successfully built"
                    }
                }
            }
        }
    }
}