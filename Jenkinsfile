pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/VvekNama/star-agile-banking-finance', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        // stage('Dockerize') {
        //     steps {
        //         sh 'docker build -t app:latest .'
        //     }
        // }
        // stage('Push Docker Image') {
        //     steps {
        //         sh 'docker tag app:latest <your-dockerhub-repo>/app:latest'
        //         sh 'docker push <your-dockerhub-repo>/app:latest'
        //     }
        // }
    //     stage('Deploy to Kubernetes') {
    //         steps {
    //             sh 'kubectl apply -f k8s-deployment.yml'
    //         }
    //     }
     }
}
