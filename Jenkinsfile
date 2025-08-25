pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'ls -l'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'ls -l'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'ls -l'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! ✅'
        }
        failure {
            echo 'Pipeline failed 💥'
        }
    }
}
