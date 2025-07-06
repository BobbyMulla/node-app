pipeline{
     agent any
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
                                    sh 'scp -r -o StrictHostKeyChecking=No ./dist/* ubuntu@3.110.188.231:/home/ubuntu/node-app/'
                                    sh 'npm start'
                                    echo "Starting development on EC2"
                                     }
                               }
                 }
         }