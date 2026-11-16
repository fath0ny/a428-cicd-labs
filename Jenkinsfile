node {
    def app

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
            withEnv(['NODE_OPTIONS=--openssl-legacy-provider']) {
                sh 'npm install'
            }
        }
    }

    stage('Test') {
        docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
            withEnv(['NODE_OPTIONS=--openssl-legacy-provider']) {
                sh './jenkins/scripts/test.sh'
            }
        }
    }

    stage('Deploy') {
        docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
            withEnv(['NODE_OPTIONS=--openssl-legacy-provider']) {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}