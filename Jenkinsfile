pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                
                git url: 'https://github.com/Nisha240/React_aws_deploy.git', branch : 'main'
            }
        }

        stage('dependency') {
            steps {
                
                sh 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                // Build the React app
                sh 'npm run build'
            }
        }
        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    scp -r ./build/* ec2-user@13.60.196.33:/var/www/html/
                    ssh ec2-user@13.60.196.33 "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }
}
