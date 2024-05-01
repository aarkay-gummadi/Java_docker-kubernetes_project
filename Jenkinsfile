pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker_cred')
    }

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
                        sh 'docker image build -t rajkumar207/productcat:latest .'
                        echo "Image successfully built"
                    }
                }
            }
        }
        stage('Updating Image On Dockerhub'){
            steps {
                script {
                    //  Pushing Image to Repository
                    withCredentials([usernameColonPassword(credentialsId: 'Docker_cred', variable: 'docker_cred')]) {
                    // some block
                    }
                }
                    sh 'docker push rajkumar207/productcat:latest'
                
                    echo "Image has been updated on dockerhub"
            }
        }
    }
}