pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/bezi2015/geolocation-eks.git'
            }
        }
        stage('Code Build') {
            steps {
                sh "mvn clean"
            }
        }
        stage('Test') {
            steps {
                sh 'make check || true'
            }
        }
    }
}
