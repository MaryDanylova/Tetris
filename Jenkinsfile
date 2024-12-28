pipeline {
    agent any

    environment {
        app_server = "ubuntu@23.20.83.29"
    }

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
                withCredentials([sshUserPrivateKey(credentialsId: 'app-server', keyFileVariable: 'app_server_key')]) {
                    sh '''
                    scp -i $app_server_key -o StrictHostKeyChecking=no -r css $app_server:/var/www/html
                    scp -i $app_server_key -o StrictHostKeyChecking=no -r images $app_server:/var/www/html
                    scp -i $app_server_key -o StrictHostKeyChecking=no -r js $app_server:/var/www/html
                    scp -i $app_server_key -o StrictHostKeyChecking=no index.html $app_server:/var/www/html/index.nginx-debian.html
                    ssh -i $app_server_key -o StrictHostKeyChecking=no $app_server "sudo systemctl restart nginx"
                    '''
                }
            }            
        }
    }
}
