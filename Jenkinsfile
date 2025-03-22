post {
    always {
        script {
            try {
                emailext (
                    subject: "Jenkins Build ${env.BUILD_NUMBER} - Status: SUCCESS",
                    body: """<p>Build ${env.BUILD_NUMBER} completed successfully.</p>
                        <p>Check console output: <a href='${env.BUILD_URL}'>Click here</a></p>""",
                    to: "keshav4788.be23@chitkara.edu.in"
                )
                echo "Email sent successfully!"
            } catch (Exception e) {
                echo "Failed to send email: ${e.getMessage()}"
            }
        }
    }
}
