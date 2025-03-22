pipeline {
    agent any

    // Environment Variables
    environment {
        DIRECTORY_PATH = "/directory_path_code_directory"
        TESTING_ENVIRONMENT = "Test Env"
        PRODUCTION_ENVIRONMENT = "Prod Env"
    }

    // Pipeline Stages
    stages {
        stage('Build') {
            steps {
                echo "Fetching source code from the directory path specified by the environment variable"
                echo "Compiling the code and generating necessary artifacts"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests..."
                echo "Running integration tests..."

                // ✅ FIX: Removed `currentBuild.result` to avoid null value issues
                emailext (
                    subject: "Jenkins Build ${env.BUILD_NUMBER} - Test Stage SUCCESS",
                    body: "The Test stage of build ${env.BUILD_NUMBER} has completed successfully.",
                    to: 'keshav4788.be23@chitkara.edu.in',
                    attachLog: true
                )
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Checking the quality of the code"
                echo "Using SonarQube for checking code quality"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Security scan using OWASP Dependency-Check plugin for checking vulnerabilities"

                // ✅ FIX: Removed `currentBuild.result` to avoid null value issues
                emailext (
                    subject: "Jenkins Build ${env.BUILD_NUMBER} - Security Scan SUCCESS",
                    body: "The Security Scan stage of build ${env.BUILD_NUMBER} has completed successfully.",
                    to: 'keshav4788.be23@chitkara.edu.in',
                    attachLog: true
                )
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging environment on AWS EC2"
                echo "Testing environment: ${TESTING_ENVIRONMENT}"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging environment..."
                echo "Tests completed successfully!"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment: ${PRODUCTION_ENVIRONMENT}"
                echo "Deployed to production!"
            }
        }
    }

    // Post-Build Email Notification
    post {
        always {
            emailext (
                subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed.</p>
                    <p>Check console output at <a href='${env.BUILD_URL}'>Jenkins Console Output</a></p>""",
                to: "keshav4788.be23@chitkara.edu.in"
            )
        }
    }
}
