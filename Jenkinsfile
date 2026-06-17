pipeline {
    agent {
        docker {
            image 'amazon/aws-cli:2.15.30'
            args '-u root' 
        }
    }
    
    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        S3_BUCKET = 'ramya-static-website'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-s3-creds', region: "${AWS_DEFAULT_REGION}") {
                    sh '''
                        aws s3 sync . s3://${S3_BUCKET} --delete --exclude ".git/*" --exclude "Jenkinsfile" --exclude "README.md"
                        echo "S3 Sync Completed"
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo "✅ Deploy Success!"
            echo "Website URL: http://${S3_BUCKET}.s3-website.${AWS_DEFAULT_REGION}.amazonaws.com"
        }
        failure {
            echo "❌ Deploy Failed. Check Console Output."
        }
    }
}
