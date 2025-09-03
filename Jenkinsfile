pipeline {
    agent any

    environment {
        AZ_API_KEY   = credentials('AZ_TOKEN')
        PROJECT_KEY  = "fUjCYsgSErEDdMizlpmUgihQulMbEFTB"
    }

    stages {
        stage('ArmourZero Security Test') {
            steps {
                script {
                    sh 'echo "Running security scan for branch: $GIT_BRANCH"'

                    sh '''
                        docker run --rm -v "$(pwd):/app/wrk" \
                          armourzero/pipe-scan:latest \
                          --apikey="$AZ_API_KEY" \
                          --projectkey="$PROJECT_KEY" \
                          --branch="$GIT_BRANCH" \
                          --repo="$GIT_URL"
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }
    }
}
