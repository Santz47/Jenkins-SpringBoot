pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Docker Build') {
            steps {
                sh 'docker build -t tp2-app:latest .'
            }
        }
        
        stage('Deploy') {
            steps {
                sh '''
                docker rm -f tp2-container || true
                docker run -d -p 8080:8080 --name tp2-container tp2-app:latest
                '''
            }
        }
    }
}
