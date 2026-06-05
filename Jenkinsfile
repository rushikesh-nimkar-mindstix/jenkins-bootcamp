pipeline {
    agent any
    environment {
        DEPLOY_ENV = "dev"
        APP_VERSION = "1.0.0"   
    }
    parameters{
        string(
            name: 'SECRET_VALUE',
            defaultValue: 'my-secret-token',
            description: 'Secret Token Value'
            )
    }
    stages {
        stage('Prepare') {
            steps {
               sh 'cat config/app-config.yaml'
            }
        }
        stage('Encode'){
            steps{
             
            script {
                env.ENCODED_TOKEN = params.SECRET_VALUE.bytes.encodeBase64().toString()
            }
        }
        }
        stage('Replace'){
            steps{

                sh "sed \
                    -e 's|__ENCODED_TOKEN__|$ENCODED_TOKEN|g' \
                    -e 's|__DEPLOY_ENV__|$DEPLOY_ENV|g' \
                    -e 's|__APP_VERSION__|$APP_VERSION|g' \
                    config/app-config.yaml > config/app-config-rendered.yaml"
               
            }
        }
        stage('Verify'){
            steps{
                sh 'cat config/app-config-rendered.yaml'
            }
        }
    }
    post{
        success{
            echo "Config rendered successfully."
        } 
        failure{
            echo "Pipeline failed at stage: check console output."
        }
    }
}