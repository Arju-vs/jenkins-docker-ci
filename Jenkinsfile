pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning source code from GitHub...'
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t task3-python-app:latest .'
            }
        }

        stage('Docker Test') {
            steps {
                echo 'Testing Docker image...'
                sh 'docker run --rm task3-python-app:latest'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline FAILED! Sending email notification...'

            emailext(
                subject: "Jenkins FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build failed.

Job: ${env.JOB_NAME}
Build Number: #${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

Please check the Jenkins console output for details.
""",
                to: 'arjunsaseendran2@gmail.com'
            )
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}
