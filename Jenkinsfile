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
            steps {
                // Run SonarQube analysis on your Python code
                withSonarQubeEnv('sonar-server') {
                    sh """
                    sonar-scanner \
                        -Dsonar.projectKey=oxy1 \
                        -Dsonar.projectName=oxy1 \
                        -Dsonar.sources=. \
                        -Dsonar.language=py \
                        -Dsonar.python.coverage.reportPaths=coverage.xml
                    """
                }
            }
        }
    }
}

