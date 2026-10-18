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
                bat '''
                    set DOCKER_HOST=npipe:////./pipe/dockerDesktopLinuxEngine
                    "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t 322824641733.dkr.ecr.ap-south-1.amazonaws.com/tickerlens:v1 .
                '''
            }
        }

        stage('Push to AWS ECR') {
            steps {
                bat '''
                    set DOCKER_HOST=npipe:////./pipe/dockerDesktopLinuxEngine
                    aws ecr get-login-password --region ap-south-1 > ecr-password.txt
                    if errorlevel 1 exit /b 1
                    "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" login --username AWS --password-stdin 322824641733.dkr.ecr.ap-south-1.amazonaws.com < ecr-password.txt
                    if errorlevel 1 exit /b 1
                    "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" push 322824641733.dkr.ecr.ap-south-1.amazonaws.com/tickerlens:v1
                    if errorlevel 1 exit /b 1
                    del ecr-password.txt
                '''
            }
        }
    }
}