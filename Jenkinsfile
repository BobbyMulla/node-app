pipeline{
     agent any
     enviornment {
          EC2_USER = 'ubuntu'
          EC2_HOST = '3.110.188.231'
          EC2_CREDENTIALS_ID = 'ec2-ssh-key'
          stages{
                 stage('build'){
                                steps{
                                    sh 'npm install'
                                    sh 'npm run build'
                                    echo "Building Complete"
                                     }
                               }
                               stage('deploy'){
                                steps{
                                   echo "Deploying to EC2"
                                    // Use SCP to copy files to EC2 instance
                                    sshagent(['ec2-ssh-key']) {
                                        sh '''
                                        echo "Copying files to EC2"
                                        scp -o StrictHostKeyChecking=No -r dist/ ubuntu@3.110.188.231:/var/www/html
                                        echo "restarting web server on ec2"
                                        echo "Starting development on EC2"
                                   '''
                                     }
                                     echo "Deployment Complete"
                                     }
                               }
                 }
         }
}