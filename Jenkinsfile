pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Application building...'
                    echo 'Tool Used: Maven/NPM'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Executing unit and integration tests...'
                    echo 'Tool Used: JUnit/TestNG'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analysing the code...'
                    echo 'Tool Used: SonarQube'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Scanning security...'
                    echo 'Tool Used: OWASP Dependency-Check/Snyk'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                    echo 'Tool Used: Docker/Kubernetes'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Executing integration tests on staging...'
                    echo 'Tool Used: Selenium/Cypress'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying production of application...'
                    echo 'Tool Used: Jenkins Pipeline/Kubernetes'
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Sending email...'
                echo 'Tool Used: Jenkins Mailer Plugin'
                mail (
                    subject: "Pipeline Notification: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                    body: "The pipeline has completed. Check details at: ${BUILD_URL}",
                    to: 'keshav4788.be23@chitkara.edu.in'
                )
            }
        }
    }
}
