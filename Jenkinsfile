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
                scp -r css ubuntu@23.20.83.29:/var/www/html
                scp -r images ubuntu@23.20.83.29:/var/www/html
                scp -r js ubuntu@23.20.83.29:/var/www/html
                scp index.html ubuntu@23.20.83.29:/var/www/html/index.nginx-debian.html
                '''
            }
        }

        stage('Restart nginx') {
            steps {
                sh '''
                ssh ubuntu@23.20.83.29 "sudo systemctl restart nginx"
                '''
            }
        }
    }
}
