pipeline {
    agent any
    
    environment {
        GITHUB_CREDENTIALS = credentials('santiagojv-github-credentials')
        AWS_ACCESS_KEY_ID = credentials('santiagojv-aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('santiagojv-aws-secret-access-key')
        S3_BUCKET = 'santiagojv-deployments'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [
                        [name: '*/main']
                    ],
                    userRemoteConfigs: [
                        [
                            url: 'https://github.com/santiago-jv/reactjs-jenkins-pipeline.git',
                            credentialsId: env.GITHUB_CREDENTIALS
                        ]
                ])
            }
        }
        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'NodeJS@16.0.0') {
                    sh 'npm i'
                    sh 'npm run build'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Must be execute tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}