pipeline {
    agent  any
    environment {
        S3_BUCKET = 'ramya-static-website'
        AWS_REGION = 'ap-south-1'
    }
    stages {
        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-s3-creds', region: 'ap-south-1') {
                    sh 'aws s3 sync . s3://${S3_BUCKET} --delete --exclude ".git/*"'
                }
            }
        }
    }
}
