pipeline {
    agent any
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
                sh 'docker tag bankfinance:latest docker.io/vvek24/bankfinance:latest'
                sh 'docker push docker.io/vvek24/bankfinance:latest'
            }
        }
        
    //     stage('Deploy to Kubernetes') {
    //         steps {
    //             sh 'kubectl apply -f k8s-deployment.yml'
    //         }
    //     }
     }
}
