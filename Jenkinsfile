
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/udayanyadav2006-a11y/TickerLens.git'
            }
        }

        stage('Check Website') {
            steps {
                bat 'if exist index.html (echo Website file found) else (exit 1)'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t tickerlens:v1 .'
            }
        }
    }
}
