
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
                    "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t udayan123/tickerlens:v1 .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '160d0519-60b0-4746-8a5d-7467d1db5934',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat '''
                        set DOCKER_HOST=npipe:////./pipe/dockerDesktopLinuxEngine
                        echo %DOCKER_PASS% | "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" login -u "%DOCKER_USER%" --password-stdin
                        "C:\\Users\\Prachi\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" push udayan123/tickerlens:v1
                    '''
                }
            }
        }
    }
}
