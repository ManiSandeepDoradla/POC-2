pipeline {
    agent any

    stages {
        stage('1. Clone Code') {
            steps {
                // Pulls code directly from your public GitHub repo
                git branch: 'main', url: 'https://github.com/ManiSandeepDoradla/POC-2.git'
            }
        }
        
        stage('2. Build & Test') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t cloud-web-app:${BUILD_NUMBER} .'
            }
        }
        
        stage('3. Deploy') {
            steps {
                echo 'Deploying Container...'
                // Removes old containers running on port 8081 if existing
                sh 'docker stop my-running-cloud-app || true'
                sh 'docker rm my-running-cloud-app || true'
                
                // Runs the application container on port 8081
                sh 'docker run -d -p 8081:80 --name my-running-cloud-app cloud-web-app:${BUILD_NUMBER}'
            }
        }
    }
}
