pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Task: Build the code using Maven'

                echo 'Tool: Maven'

            }

        }

        stage('Unit and Integration Tests') {

            steps {

                echo 'Task: Run unit tests using JUnit and integration tests using TestNG'

                echo 'Tools: JUnit, TestNG'

            }

        }

        stage('Code Analysis') {

            steps {

                echo 'Task: Analyze the code using SonarQube'

                echo 'Tool: SonarQube'

            }

        }

        stage('Security Scan') {

            steps {

                echo 'Task: Perform security scan using OWASP Dependency-Check'

                echo 'Tool: OWASP Dependency-Check'

            }

        }

        stage('Deploy to Staging') {

            steps {

                echo 'Task: Deploy the application to a staging server using AWS CLI'

                echo 'Tool: AWS CLI'

            }

        }

        stage('Integration Tests on Staging') {

            steps {

                echo 'Task: Run integration tests on the staging environment using Postman'

                echo 'Tool: Postman'

            }

        }

        stage('Deploy to Production') {

            steps {

                echo 'Task: Deploy the application to a production server using AWS CLI'

                echo 'Tool: AWS CLI'

            }

        }

    }

    post {

        always {

            echo 'Pipeline finished'

        }

        success {

            script {
                def logFile = "pipeline-logs-success-${currentBuild.number}.txt"
                sh "cat ${env.WORKSPACE}/build.log > ${logFile}"
                emailext(
                    to: 'miguelimperial020@gmail.com',
                    subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                    body: "The pipeline has completed successfully. Please find the logs attached.",
                    attachLog: true,
                    attachmentsPattern: logFile
                )
            }
        }

        failure {

            script {
                def logFile = "pipeline-logs-failure-${currentBuild.number}.txt"
                sh "cat ${env.WORKSPACE}/build.log > ${logFile}"
                emailext(
                    to: 'miguelimperial020@gmail.com',
                    subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                    body: "The pipeline has failed. Please check the Jenkins console output. Logs are attached.",
                    attachLog: true,
                    attachmentsPattern: logFile
                )
            }
        }

    }

}
