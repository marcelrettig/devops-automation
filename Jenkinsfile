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
                    docker.build('vote', './vote/Dockerfile .')
                    docker.build('result', './result/Dockerfile .')
                    docker.build('worker', './worker/Dockerfile .')
                    docker.withRegistry('https://index.docker.io/v1/', 'f0a1de77-ecbe-4b26-842d-1cf7345df720') {
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
