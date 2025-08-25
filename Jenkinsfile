pipeline {
    agent any
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: true, description: 'Should we deploy?')
    }
    stages {
        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
