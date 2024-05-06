pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout des Codes aus dem GitHub-Repository
                git branch: 'main', url:'https://github.com/marcelrettig/devops-automation.git'
            }
        }
        
        stage('Build and Push Images') {
            steps {
                // Baue und pushe die Docker-Images
                script {
                    docker.build('vote', './vote')
                    docker.build('result', './result')
                    docker.build('worker', './worker')
                    docker.withRegistry('https://hub.docker.com/repository/docker/rettig/devops-automation', 'f304fd37-5fe3-4a9a-8755-15e29975fd8a') {
                        docker.image('vote').push('latest')
                        docker.image('result').push('latest')
                        docker.image('worker').push('latest')
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy der Anwendung mit Docker-Compose
                sh 'docker-compose up -d'
            }
        }
    }
}
