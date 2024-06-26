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
        stage ('Building New Docker Image stockmanager') {
            steps {
                script {
                    dir('./shopfront') {
                        //  Building new image
                        sh 'mvn clean install -DskipTests'
                        sh 'docker image build -t rajkumar207/stockman:latest .'
                        echo "Image successfully built"
                    }
                }
            }
        }
        stage('Updating Image On Dockerhub of stockmanager'){
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push rajkumar207/stockman:latest'
                
                    echo "Image has been updated on dockerhub"
                    
                }
                    
            }
        }
        stage('minikube starting') {
            steps {
                sh 'curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb'
                sh 'sudo dpkg -i minikube_latest_amd64.deb'
                sh 'minikube start'
            }
        }
        stage ('installing kubectl') {
            steps {
                sh 'sudo snap install kubectl --classic'
                echo 'installed kubectl successfully'
            }
        }
        stage ('deploy k8s') {
            steps {
                script {
                    dir('./kubernetes') {
                        sh 'kubectl apply -f productcatalogue-service.yaml'
                        sh 'kubectl apply -f shopfront-service.yaml'
                        sh 'kubectl apply -f stockmanager-service.yaml'
                    }
                }
            }
        }
        stage ('know the service individuals') {
            steps {
                sh 'minikube service productcatalogue'
                sh 'minikube service shopfront'
                sh 'minikube service stockmanager'
            }
        } 
    }
}