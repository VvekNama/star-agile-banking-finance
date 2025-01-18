pipeline {
    agent any
    
environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-pat') 
        DOCKER_IMAGE_NAME = 'bankfinance:latest'
        DOCKERHUB_REPO = 'vvek24/bankfinance'
       // K8S_TOKEN = credentials('k8s-token')
        KUBECONFIG = credentials('k8s-token')
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

             script {
                    // Apply your deployment
                    sh "kubectl --kubeconfig=${KUBECONFIG} apply -f k8s/deployment.yml  --validate=false"
                                
               // script {
               //      withCredentials([string(credentialsId: 'k8s-token', variable: 'K8S_TOKEN')]) {
               //          // Now the token is safely injected as an environment variable
               //          sh "kubectl --token=\${K8S_TOKEN} apply -f k8s/deployment.yml --validate=false"
                // }
                }
                // sh 'kubectl apply -f k8s/deployment.yml --validate=false'
                // sh 'kubectl apply -f k8s/service.yml --validate=false'
            }
        }
     }
}
