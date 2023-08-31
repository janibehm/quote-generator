pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t janibehm/quote-generator:latest .'
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                sh "echo \${DOCKERHUB_CREDENTIALS_PSW} | docker login -u \${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                sh 'docker push janibehm/quote-generator:latest'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh "chmod +x -R ./scripts/test.sh"
                sh './scripts/test.sh'
            }
        }
        
        stage('Deliver') {
            steps {
                sh "chmod +x ./scripts/deliver.sh"
                sh './scripts/deliver.sh'
                input message: 'Finished using the quote-generator app? (Click "Proceed" to continue)'
                sh "chmod +x ./scripts/kill.sh"
                sh './scripts/kill.sh'
            }
        }
    }
}
