pipeline {
    agent any
    
environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-pat') 
        DOCKER_IMAGE_NAME = 'bankfinance:latest'
        DOCKERHUB_REPO = 'vvek24/bankfinance'
       // K8S_TOKEN = credentials('k8s-token')
        // KUBECONFIG = credentials('k8s-token')
        KUBECONFIG = credentials('k8s-token') 
        }
    
    stages {
        stage('Clone Repository') {
            // steps {
            //     git url: 'https://github.com/VvekNama/star-agile-banking-finance', branch: 'master'
            //     credentialsId: 'github-token'

                 steps {
                git(
                    url: 'https://github.com/VvekNama/star-agile-banking-finance', branch: 'master',
                    credentialsId: 'github-token'
                )
            
                
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


         stage('Run Docker Container') {
            steps {
                script {
                    // Run the container in detached mode
                    sh """
                        docker run -d --name finance-container -p 8081:8081 ${DOCKER_IMAGE_NAME}
                    """
                }
            }
        }
        
        // stage('Deploy to Kubernetes') {
        //     steps {

        //      script {
        //             // Decode kubeconfig and apply deployment
        //             sh '''#!/bin/bash
        //             echo "$KUBECONFIG" | base64 -d > /tmp/kubeconfig
        //             kubectl --kubeconfig=/tmp/kubeconfig apply -f k8s/deployment.yml --validate=false
        //             '''
        //         }
                
        //         // sh 'kubectl apply -f k8s/deployment.yml --validate=false'
        //         // sh 'kubectl apply -f k8s/service.yml --validate=false'
        //     }
        // }
     }
}
