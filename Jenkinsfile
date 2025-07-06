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
                                    sh 'scp -r -o strictCheckingOfKey=No ./dist/* /home/ubuntu/node-app/'
                                    sh 'npm start'
                                    echo "Starting development on EC2"
                                     }
                               }
                 }
         }