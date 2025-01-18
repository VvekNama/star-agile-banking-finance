pipeline {
    agent any
    
environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-pat') 
        DOCKER_IMAGE_NAME = 'bankfinance:latest'
        DOCKERHUB_REPO = 'vvek24/bankfinance'
        }
    
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/VvekNama/star-agile-banking-finance', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Dockerize') {
            steps {
                sh 'docker build -t bankfinance:latest .'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                sh """
                    echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                    docker tag ${DOCKER_IMAGE_NAME} ${DOCKERHUB_REPO}
                    docker push ${DOCKERHUB_REPO}
                """
                
                sh 'docker tag bankfinance:latest docker.io/vvek24/bankfinance:latest'
                sh 'docker push docker.io/vvek24/bankfinance:latest'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yml'
                sh 'kubectl apply -f k8s/service.yml'
            }
        }
     }
}
