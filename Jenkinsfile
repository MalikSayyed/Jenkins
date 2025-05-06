pipeline {
    agent any


    environment {
        S3_BUCKET_NAME = 'my-static-websitss '  // The name of your S3 bucket
        REGION = 'us-east-1'  // Region where your S3 bucket is located
    }


    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository containing your website files
                git 'https://github.com/MalikSayyed/Jenkins'
            }
        }


        stage('Deploy to S3') {
            steps {
                script {
                    // Using the credentials stored in Jenkins
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'b032e0aa-a960-4f24-a729-929ecd864aac']]) {
                        // Sync the current directory (where the files are cloned) to S3
                        sh """
                        echo "Deploying to S3 bucket ${S3_BUCKET_NAME}"
                        aws s3 sync . s3://${S3_BUCKET_NAME}/ --region ${REGION} --delete
                        """
                    }
                }
            }
        }
    }
}
