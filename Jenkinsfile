pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Python code from your version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Static Code Analysis') {
            def scannerHome = tool 'somscanner';
            withSonarQubeEnv('sonar-server') {
                    sh """
                    sonar-scanner \
                        -Dsonar.projectKey=oxy1 \
                        -Dsonar.projectName=oxy1 \
                        -Dsonar.sources=. \
                        -Dsonar.language=py \
                        
                    """
                
            }
        }
    }
}

