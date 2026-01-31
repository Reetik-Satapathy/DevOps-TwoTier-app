pipeline {
    agent any

    environment {
        FLASK_APP_HOST = "3.82.57.210"
        APP_DIR = "/home/ubuntu/DevOps-TwoTier-app"
    }

    stages {
        stage('Deploy to Flask EC2') {
            steps {
                sshagent(credentials: ['flaskapp-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ubuntu@${FLASK_APP_HOST} "
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
