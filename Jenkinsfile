node {
    def app

    stage('Checkout') {
        checkout scm
    }

    docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
        withEnv(['NODE_OPTIONS=--openssl-legacy-provider']) {
            stage('Build') {
                sh 'npm install'
            }

            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }

            stage('Manual Approval') {
                input message: 'Lanjutkan ke tahap Deploy? (Proceed untuk lanjut, Abort untuk membatalkan)'
            }

            stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                echo 'Menjalankan proses selama 1 menit'
                sleep(60)
                echo 'Proses selesai dalam 1 menit'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}