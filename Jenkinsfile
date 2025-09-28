pipeline {
    agent { label 'master' }

    environment {
        USERNAME = "alizamangi"
        SERVER = "192.168.56.105"
        DEPLOY_PATH = "/var/www/mysite-ui"
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:student-Alizaa/mysite-ui.git',
                    credentialsId: 'github-ssh-key'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                    rsync -avz --exclude ".git/" --exclude "Jenkinsfile" ${WORKSPACE}/ ${USERNAME}@${SERVER}:${DEPLOY_PATH}/
                    ssh ${USERNAME}@${SERVER} "sudo systemctl restart apache2"
                '''
            }
        }
    }
}
