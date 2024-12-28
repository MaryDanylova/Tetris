pipeline {
    agent any

    stages {        
        stage('List files in repo') {
            steps {
                sh '''
                ls -lah
                '''
            }
        }

        stage('Deploy the app') {
            steps {
                sh '''
                scp -i /home/ubuntu/.ssh/id_ed25519 -r css ubuntu@23.20.83.29:/var/www/html
                scp -i /home/ubuntu/.ssh/id_ed25519 -r images ubuntu@23.20.83.29:/var/www/html
                scp -i /home/ubuntu/.ssh/id_ed25519 -r js ubuntu@23.20.83.29:/var/www/html
                scp -i /home/ubuntu/.ssh/id_ed25519 index.html ubuntu@23.20.83.29:/var/www/html/index.nginx-debian.html
                '''
            }
        }

        stage('Restart nginx') {
            steps {
                sh '''
                ssh -i /home/ubuntu/.ssh/id_ed25519 ubuntu@23.20.83.29 "sudo systemctl restart nginx"
                '''
            }
        }
    }
}
