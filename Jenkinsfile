pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'mvn -B clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-demo:latest .'
            }
        }
    }

    post {
        success {
            echo 'Lab 16: Build completed successfully.'
        }
        failure {
            echo 'Lab 16: Build failed. Check Console Output.'
        }
    }
}
