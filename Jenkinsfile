pipeline {
    agent any

    environment {
        EC2_USER = 'ubuntu'
        EC2_HOST = '3.110.188.231'
        EC2_CREDENTIALS_ID = 'ec2-ssh-key'
    }

    stages {
        stage('build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                echo 'Building Complete'
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploying to EC2'

                sshagent(credentials: [env.EC2_CREDENTIALS_ID]) {
                    sh '''
                    echo "Copying files to EC2"
                    scp -o StrictHostKeyChecking=no -r dist/* ubuntu@52.66.245.109: /home/ubuntu/dist

                    echo "Restarting web server on EC2"
                    ssh -o StrictHostKeyChecking=no ubuntu@52.66.245.109: 'sudo mv /home/ubuntu/dist/* /var/www/html && sudo systemctl restart nginx'
                    
                    echo "Deployment finished on EC2"
                    '''
                }

                echo 'Deployment Complete'
            }
        }
    }
}
