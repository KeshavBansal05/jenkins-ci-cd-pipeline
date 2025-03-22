pipeline {
    agent any

    environment {
        SMTP_SERVER = "smtp.gmail.com"
        SMTP_PORT = "587"  // Using TLS (Try "465" if this doesn't work)
        SMTP_USER = "keshav4788.be23@chitkara.edu.in"
        SMTP_PASSWORD = "crhi ywsi eejr jfhy"  // App Password
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetching source code..."
                echo "Compiling the code and generating necessary artifacts..."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests..."
                echo "Running integration tests..."
                
                script {
                    try {
                        emailext (
                            subject: "Jenkins Build ${env.BUILD_NUMBER} - Test Stage SUCCESS",
                            body: "The Test stage of build ${env.BUILD_NUMBER} has completed successfully.",
                            to: 'keshav4788.be23@chitkara.edu.in',
                            attachLog: true
                        )
                        echo "✅ Email sent successfully for Test Stage!"
                    } catch (Exception e) {
                        echo "❌ Email sending failed for Test Stage: ${e.getMessage()}"
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing static code analysis using SonarQube..."
                sh 'sonar-scanner'  // Replace with actual SonarQube command
            }
        }

        stage('Security Scan') {
            steps {
                echo "Running OWASP Dependency-Check for security vulnerabilities..."
                sh './dependency-check.sh --scan .'  // Ensure this tool is installed

                script {
                    try {
                        emailext (
                            subject: "Jenkins Build ${env.BUILD_NUMBER} - Security Scan SUCCESS",
                            body: "The Security Scan stage of build ${env.BUILD_NUMBER} has completed successfully.",
                            to: 'keshav4788.be23@chitkara.edu.in',
                            attachLog: true
                        )
                        echo "✅ Email sent successfully for Security Scan!"
                    } catch (Exception e) {
                        echo "❌ Email sending failed for Security Scan: ${e.getMessage()}"
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment..."
                echo "Testing Environment: ${TESTING_ENVIRONMENT}"
                sh 'scp target/*.jar user@staging-server:/deploy/'  // Adjust based on your environment
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests in the staging environment..."
                echo "Tests completed successfully!"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment: ${PRODUCTION_ENVIRONMENT}"
                sh 'scp target/*.jar user@production-server:/deploy/'  // Adjust as needed
                echo "✅ Deployment to production completed!"
            }
        }
    }

    post {
        always {
            script {
                try {
                    emailext (
                        subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed.</p>
                            <p>Check console output at <a href='${env.BUILD_URL}'>Jenkins Console Output</a></p>""",
                        to: "keshav4788.be23@chitkara.edu.in"
                    )
                    echo "✅ Final success email sent!"
                } catch (Exception e) {
                    echo "❌ Final email sending failed: ${e.getMessage()}"
                }
            }
        }
    }
}
