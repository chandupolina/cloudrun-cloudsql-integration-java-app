pipeline {
    agent any // Run on any available agent

    // Environment variables for configuration
    environment {
        SONAR_SERVER          = 'sonarqube-server'          // Your SonarQube server name in Jenkins
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'    // Jenkins credentials ID for your Docker registry
        DOCKER_USERNAME       = 'your-docker-username'      // Your Docker Hub username or registry namespace
        IMAGE_NAME            = 'my-app'                    // The name for your Docker image
    }

    stages {


        // Stage 1: Build the application
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Replace with your build command (e.g., 'npm install')
                sh 'mvn clean install'
            }
        }


        // Stage 2: Scan with SonarQube
        stage('SonarQube Scan') {
            steps {
                echo 'Running SonarQube analysis...'
                // Sets up SonarQube environment
                withSonarQubeEnv(SONAR_SERVER) {
                    // Runs the scanner
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    // Runs after the pipeline finishes
    post {
        always {
            echo 'Pipeline finished.'
            cleanWs() // Clean up the workspace
        }
    }
}
