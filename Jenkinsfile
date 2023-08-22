pipeline {
    agent any

    environment {
        // Define your environment variables
        AWS_REGION = 'us-east-1' // Replace with your AWS region
        ECR_REGISTRY = 'ECR_REGISTRY' // Replace with your ECR repository name
        IMAGE_NAME = 'image' // Replace with your Docker image name
        GIT_REPO_URL = 'https://github.com/amrutha2234/repo-2.git'
	IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone code from GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/amrutha2234/repo-2.git']]])
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                sh "docker build -t ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

      

        stage('Push to ECR') {
            steps {
                // Push the Docker image to ECR
		sh "docker push ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}
        }
    
}

