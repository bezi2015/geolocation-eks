pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {
        registry = '070285518813.dkr.ecr.us-east-1.amazonaws.com/geolocation_ecr_rep'
        dockerimage = '' 
    }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/bezi2015/geolocation-eks.git'
            }
        }
        stage('Code Build') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('Test') {
            steps {
                sh 'make check || true'
            }
        }
        // Building Docker images
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
            steps{
                script {
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 070285518813.dkr.ecr.us-east-1.amazonaws.com'
                    sh 'docker push 070285518813.dkr.ecr.us-east-1.amazonaws.com/geolocation_ecr_rep:latest'
                }
            }
        }
    }
}
