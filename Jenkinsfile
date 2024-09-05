pipeline {
    agent any
    tools {
        maven 'Maven'  // This assumes you have Maven configured in Jenkins Global Tool Configuration
    }
    stages {
        stage('Build') {
            steps {
                echo 'Task: Build the code using Maven'
                bat 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests using JUnit and integration tests using TestNG'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Analyze the code using SonarQube'
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Perform security scan using OWASP Dependency-Check'
                bat 'mvn org.owasp:dependency-check-maven:check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy the application to a staging server using AWS CLI'
                bat 'echo Simulating deployment to staging'
                // Uncomment and adjust when ready to use actual AWS CLI commands
                // bat 'aws deploy create-deployment --application-name YourApp --deployment-group-name Staging --s3-location s3://your-bucket/your-app.zip'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run integration tests on the staging environment using Postman'
                bat 'echo Simulating Postman tests'
                // Uncomment when ready to use actual Postman/Newman commands
                // bat 'newman run your_postman_collection.json -e staging_environment.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy the application to a production server using AWS CLI'
                bat 'echo Simulating deployment to production'
                // Uncomment and adjust when ready to use actual AWS CLI commands
                // bat 'aws deploy create-deployment --application-name YourApp --deployment-group-name Production --s3-location s3://your-bucket/your-app.zip'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            echo 'Pipeline succeeded'
            mail to: 'miguelimperial020@gmail.com',
                 subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                 body: "The pipeline has completed successfully."
        }
        failure {
            echo 'Pipeline failed'
            mail to: 'miguelimperial020@gmail.com',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline has failed. Please check the Jenkins console output for details."
        }
    }
}
