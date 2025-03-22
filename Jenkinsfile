pipeline {
    agent any

    environment {
        SMTP_SERVER = "smtp.gmail.com"
        SMTP_PORT = "587"  // Using TLS
        SMTP_USER = "keshav4788.be23@chitkara.edu.in"
        SMTP_PASSWORD = "crhi ywsi eejr jfhy"  // App Password
    }

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo "Building code..."
            }
        }

        // Stage 2: Unit Tests
        stage('Unit Tests') {
            steps {
                echo "Running unit tests..."
            }
            post {
                always {
                    script {
                        try {
                            emailext (
                                subject: "Jenkins Build ${env.BUILD_NUMBER} - Unit Test Results: SUCCESS",
                                body: "Unit tests completed successfully!",
                                to: "keshav4788.be23@chitkara.edu.in",
                                replyTo: "keshav4788.be23@chitkara.edu.in"
                            )
                            echo "✅ Unit Test email sent!"
                        } catch (Exception e) {
                            echo "❌ Failed to send Unit Test email: ${e.getMessage()}"
                        }
                    }
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo "Checking code quality..."
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo "Scanning for vulnerabilities..."
            }
            post {
                always {
                    script {
                        try {
                            emailext (
                                subject: "Jenkins Build ${env.BUILD_NUMBER} - Security Scan Results: SUCCESS",
                                body: "Security scan completed successfully!",
                                to: "keshav4788.be23@chitkara.edu.in"
                            )
                            echo "✅ Security Scan email sent!"
                        } catch (Exception e) {
                            echo "❌ Failed to send Security Scan email: ${e.getMessage()}"
                        }
                    }
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging..."
            }
        }

        // Stage 6: Integration Tests
        stage('Integration Tests') {
            steps {
                echo "Running integration tests..."
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production..."
            }
        }
    }

    post {
        always {
            script {
                try {
                    emailext (
                        subject: "Jenkins Build ${env.BUILD_NUMBER} - SUCCESS",
                        body: """<p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed successfully.</p>
                                 <p>Check console output: <a href='${env.BUILD_URL}'>Jenkins Console Output</a></p>""",
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
