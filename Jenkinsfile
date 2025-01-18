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
                sh 'docker build -t BankFinance:latest .'
            }
        }
        // stage('Push Docker Image') {
        //     steps {
        //         sh 'docker tag BankFinance:latest VvekNama/BankFinance:latest'
        //         sh 'docker push VvekNama/BankFinance:latest'
        //     }
        // }
    //     stage('Deploy to Kubernetes') {
    //         steps {
    //             sh 'kubectl apply -f k8s-deployment.yml'
    //         }
    //     }
     }
}
