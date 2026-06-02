pipeline {
    agent any
    stages {
        stage('Hello this is new message') {
            steps {
                echo "Running from SCM — branch: ${env.GIT_BRANCH}"
                echo "Commit: ${env.GIT_COMMIT}"
                sh 'ls -la'
            }
        }
    }
}