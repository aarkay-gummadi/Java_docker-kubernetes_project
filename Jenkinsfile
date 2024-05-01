pipeline {
    agent any
    stages {
        stage ('git checkout') {
            steps {
                sh 'rm -rf Java_docker-kubernetes_project'

                sh 'git clone https://github.com/aarkay-gummadi/Java_docker-kubernetes_project.git'

            }
        }
        stage ('Building New Docker Image') {
            steps {
                script {
                    dir('./productcatalogue') {
                        //  Building new image
                        sh 'mvn clean install'
                        sh 'docker image build -t $DOCKER_HUB_REPO:$BUILD_NUBMER .'
                        echo "Image successfully built"
                    }
                }
            }
        }
    }
}