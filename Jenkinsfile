pipeline {
    agent any

    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Select deployment environment')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'sleep 2'
            }
        }

        stage('Test in Parallel') {
            parallel {
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 2'
                    }
                }
            }
        }

        stage('Simulate Testing (Parallel)') {
            parallel {
                stage('Linux') {
                    agent { label 'linux' }
                    steps {
                        echo 'Simulating tests on Linux'
                    }
                }
                stage('Windows') {
                    agent { label 'windows' }
                    steps {
                        echo 'Simulating tests on Windows'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo "All tests passed!" > results.txt'
                archiveArtifacts artifacts: 'results.txt', fingerprint: true
            }
        }

        stage('Approval') {
            agent none
            steps {
                input message: "Do you want to proceed with deployment?"
            }
        }

        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo "Deploying application to ${params.ENVIRONMENT} environment..."
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
