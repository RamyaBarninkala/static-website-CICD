pipeline {
    agent {
        docker { 
            image 'amazon/aws-cli' 
            args '-u root' // permission kosam
        }
    }
    environment {
        S3_BUCKET = 'ramya-static-website'
    }
    stages {
        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-s3-creds', region: 'ap-south-1') {
                    sh 'aws s3 sync . s3://$S3_BUCKET --delete --exclude ".git/*"'
                }
            }
        }
    }
}
