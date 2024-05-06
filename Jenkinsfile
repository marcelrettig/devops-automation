stage('Build and Push Images') {
    steps {
        // Baue und pushe die Docker-Images
        script {
            docker.build('vote', './vote')
            docker.build('result', './result')
            docker.build('worker', './worker')
            docker.withRegistry('https://index.docker.io/v1/', 'f0a1de77-ecbe-4b26-842d-1cf7345df720') {
                docker.image('vote').push('latest')
                docker.image('result').push('latest')
                docker.image('worker').push('latest')
            }
        }
    }
}
