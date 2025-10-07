pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        S3_BUCKET = 'jitendra-demo1'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Jitendrapatelnb/my-website1.git', branch: 'main'
            }
        }
        stage('Deploy to S3') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'deploy-credentials', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh '''
                        aws s3 sync . s3://$S3_BUCKET --delete --exclude ".git" --exclude "Jenkinsfile"
                    '''
                }
            }
        }
    }
}
