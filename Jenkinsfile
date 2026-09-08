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
            echo 'CI Pipeline FAILED!'
            // Email/Slack notification will be configured later
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}
