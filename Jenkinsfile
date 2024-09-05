pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Task: Build the code using Maven'
                echo 'Tool: Maven'
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests using JUnit and integration tests using TestNG'
                echo 'Tools: JUnit, TestNG'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Analyze the code using SonarQube'
                echo 'Tool: SonarQube'
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Perform security scan using OWASP Dependency-Check'
                echo 'Tool: OWASP Dependency-Check'
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy the application to a staging server using AWS CLI'
                echo 'Tool: AWS CLI'
                sh 'aws deploy create-deployment --application-name YourApp --deployment-group-name Staging --s3-location s3://your-bucket/your-app.zip'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run integration tests on the staging environment using Postman'
                echo 'Tool: Postman'
                sh 'newman run your_postman_collection.json -e staging_environment.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy the application to a production server using AWS CLI'
                echo 'Tool: AWS CLI'
                sh 'aws deploy create-deployment --application-name YourApp --deployment-group-name Production --s3-location s3://your-bucket/your-app.zip'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished'
            script {
                def logContent = currentBuild.rawBuild.getLog(10000).join('\n')
                writeFile file: 'pipeline.log', text: logContent
            }
        }
        success {
            emailext to: 'miguelimperial020@gmail.com',
                     subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                     body: "The pipeline has completed successfully.",
                     attachmentsPattern: 'pipeline.log'
        }
        failure {
            emailext to: 'miguelimperial020@gmail.com',
                     subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                     body: "The pipeline has failed. Please check the attached logs.",
                     attachmentsPattern: 'pipeline.log'
        }
    }
}
