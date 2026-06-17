pipeline {
    agent any
    environment {
        S3_BUCKET = 'ramya-static-website'
        AWS_REGION = 'ap-south-1'
    }
    stages {
        stage('Deploy to S3') {
            steps {
                sh '''
                    export AWS_ACCESS_KEY_ID=$(echo $AWS_ACCESS_KEY_ID)
                    export AWS_SECRET_ACCESS_KEY=$(echo $AWS_SECRET_ACCESS_KEY)
                    aws s3 sync . s3://${S3_BUCKET} --delete --exclude ".git/*" --region ${AWS_REGION}
                '''
            }
        }
    }
}
