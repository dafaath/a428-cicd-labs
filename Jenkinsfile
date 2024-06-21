node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') { 
        stage('Build') {
            sh 'npm install' 
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Deploy') {
            // Create an Approval Button with a timeout of 15minutes.
            timeout(time: 15, unit: "MINUTES") {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }

            sh './jenkins/scripts/deliver.sh'
            sleep(60)
            sh './jenkins/scripts/kill.sh'
        }
    }
}