node {
    def app

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }
}