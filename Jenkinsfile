pipeline {
    agent any

    environment {
        PORT = '5000'
        AWS_REGION = 'us-east-1'
        S3_BUCKET_NAME = 'miniwetransfer-uploads-nilad-demo-123'
        DYNAMODB_TABLE_NAME = 'MiniWeTransferFiles'
        SES_SENDER_EMAIL = 'niladrirah@gmail.com'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
                echo 'Source code checked out successfully.'
            }
        }

        stage('Configure Environment') {
            steps {
                withCredentials([
                    string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS'),
                    string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET')
                ]) {
                    sh '''
                    echo "PORT=${PORT}" > backend/.env
                    echo "AWS_ACCESS_KEY_ID=${AWS_ACCESS}" >> backend/.env
                    echo "AWS_SECRET_ACCESS_KEY=${AWS_SECRET}" >> backend/.env
                    echo "AWS_REGION=${AWS_REGION}" >> backend/.env
                    echo "S3_BUCKET_NAME=${S3_BUCKET_NAME}" >> backend/.env
                    echo "DYNAMODB_TABLE_NAME=${DYNAMODB_TABLE_NAME}" >> backend/.env
                    echo "SES_SENDER_EMAIL=${SES_SENDER_EMAIL}" >> backend/.env
                    '''
                    echo 'Environment file (.env) generated successfully.'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker-compose build'
                echo 'Docker images built successfully.'
            }
        }

        stage('Deploy to Environment') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
                echo 'Application successfully deployed using Docker Compose.'
            }
        }
    }

    post {
        always {
            // Clean up old Docker images to save disk space
            sh 'docker image prune -f || true'
            echo 'Pipeline execution complete.'
        }
        success {
            echo '✅ Deployment successful! Your Mini-WeTransfer app is live.'
        }
        failure {
            echo '❌ Deployment failed. Please check the Jenkins logs for errors.'
        }
    }
}
