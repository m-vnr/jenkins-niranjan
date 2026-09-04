pipeline {
    agent any

    parameters {
        string(name: 'APP_NAME', defaultValue: 'my-first-app', description: 'Name of the application')
        choice(name: 'ENVIRONMENT', choices: ['development', 'staging', 'production'], description: 'Where to deploy')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building ${params.APP_NAME} on the DEVELOP branch..."
                sh 'echo "This file was created during Build" > output.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'cat output.txt'
            }
        }
        stage('Deploy') {
            when {
                expression { params.ENVIRONMENT == 'production' }
            }
            steps {
                echo "Deploying ${params.APP_NAME} to ${params.ENVIRONMENT}..."
            }
        }
    }

    post {
        success {
            echo "Pipeline for ${params.APP_NAME} finished successfully!"
        }
        always {
            echo 'This always runs, no matter what.'
        }
    }
}
