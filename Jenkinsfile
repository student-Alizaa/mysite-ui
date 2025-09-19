pipeline {
    agent any

    environment {
        USERNAME = "alizamangi"
        SERVER = "192.168.56.105"
        DEPLOY_PATH = "/var/www/test"
    }

    stages {
        stage('Deploy to Apache') {
            steps {
                sh """
                    rsync -av --exclude ".git/" --exclude "Jenkinsfile" ${WORKSPACE}/* ${USERNAME}@${SERVER}:${DEPLOY_PATH}/
                    ssh ${USERNAME}@${SERVER} 'systemctl --user restart apache2'
                """
            }
        }
    }
}
