pipeline {
    agent any

    environment {
        FLASK_APP_HOST = "172.31.65.80"
        APP_DIR = "/home/ubuntu/DevOps-Project-Two-Tier-App"
    }

    stages {
        stage('Deploy to Flask EC2') {
            steps {
                sshagent(credentials: ['flaskapp-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o BatchMode=yes ubuntu@${FLASK_APP_HOST} "
                            set -e
                            cd ${APP_DIR}
                            git pull origin main
                            docker compose down
                            docker compose up -d --build
                        "
                    '''
                }
            }
        }
    }
}
