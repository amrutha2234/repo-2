pipeline {
    agent any

    environment {
        // Define environment variables for your Git repository and ECR.
        GIT_REPO_URL = 'git@github.com:amrutha2243/repo-2.git'
        ECR_REGISTRY = 'ECR_REGISTRY'
        IMAGE_NAME = 'img1'
    }

    stages {
        stage('Clone Code') {
            steps {
                // Checkout code from Git repository.
                git branch: 'main', git url: "${GIT_REPO_URL}", credentialsId: 'prvtkey'
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build and tag the Docker image.
                    dockerImage = docker.build("${ECR_REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}")

                    // Authenticate with AWS ECR using credentials.
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY',
                        credentialsId: 'keyforecr'
                    ]]) {
                        // Push the Docker image to ECR.
                        docker.withRegistry(ECR_REGISTRY, 'ecr:us-east-1') {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}

