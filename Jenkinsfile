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
                scp -r . ubuntu@23.20.83.29:/var/www/html                
                '''
            }
        }

        stage('Restart nginx') {
            steps {
                sh '''
                ssh ubuntu@23.20.83.29 -c sudo systemctl restart nginx
                '''
            }
        }
    }
}
