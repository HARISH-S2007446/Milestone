pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'python -m py_compile app.py'
                sleep time: 15, unit: 'SECONDS'
            }
        }
        stage('Send Notification') {
            steps {
                script {
                    def recipient = 'harish@gmail.com'
                    def subject = "${env.JOB_NAME} - Build #${env.BUILD_NUMBER}"
                    def body = "Build URL: ${env.BUILD_URL}"
                    try {
                        mail(
                            to: recipient,
                            subject: subject,
                            body: body
                        )
                    } catch (Exception ex) {
                        echo "SMTP notification unavailable: ${ex.message}"
                        echo "To: ${recipient}"
                        echo "Subject: ${subject}"
                        echo "Body: ${body}"
                    }
                }
            }
        }
    }
}