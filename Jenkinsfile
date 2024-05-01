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
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push rajkumar207/productcat:latest'
                
                    echo "Image has been updated on dockerhub"
                    
                }
                    
            }
        }
        stage ('Building New Docker Image shopfront') {
            steps {
                script {
                    dir('./shopfront') {
                        //  Building new image
                        sh 'mvn clean install -DskipTests'
                        sh 'docker image build -t rajkumar207/shopfr:latest .'
                        echo "Image successfully built"
                    }
                }
            }
        }
        stage('Updating Image On Dockerhub of shfr'){
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push rajkumar207/shopfr:latest'
                
                    echo "Image has been updated on dockerhub"
                    
                }
                    
            }
        }
    }
}