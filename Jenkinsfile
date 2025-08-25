pipeline {
    agent any

    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Simulate Testing (Parallel)') {
            parallel {
                stage('Linux') {
                    agent { label 'linux' }
                    steps {
                        echo 'Simulating tests on Linux'
                        sh 'echo "Linux tests done"'
                    }
                }
                stage('Windows') {
                    agent { label 'windows' }
                    steps {
                        echo 'Simulating tests on Windows'
                        bat 'echo Windows tests done'
                    }
                }
            }
        }

        stage('Test in Parallel') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 2'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 2'
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
            when { beforeAgent true }
            steps {
                input message: "Do you want to proceed with deployment?"
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
