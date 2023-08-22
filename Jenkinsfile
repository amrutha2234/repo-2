pipeline {
    agent {
        // Specify an appropriate agent type, e.g., 'docker' or 'kubernetes'
        // agent_type 'docker'
    }

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY = 'ECR_REGISTRY'
        IMAGE_NAME = 'your-image-name'
        GIT_REPO_URL = 'https://github.com/amrutha2234/repo-2.git'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: GIT_REPO_URL]]])
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image, specify Dockerfile path
                sh "docker build -t ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push to ECR') {
            steps {
                // Log in to ECR using AWS credentials
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'keyforecr',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    sh "docker login -u AWS -p ${AWS_ACCESS_KEY_ID} https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
                    sh "docker push ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}

