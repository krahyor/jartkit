pipeline {
    agent any
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
    }
    stages {
        stage('Test') {
            steps {
                sh 'echo "All tests passed!" > results.txt'
                archiveArtifacts artifacts: 'results.txt', fingerprint: true
            }
        }
        stage('Approval') {
            steps {
                input "Do you want to proceed with deployment?"
            }
        }
        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo 'Deploying application...'
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs!'
        }
        always {
            echo 'Pipeline completed (success or failure).'
        }
    }
}
