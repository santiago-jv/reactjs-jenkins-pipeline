pipeline {
    agent any 
    environment {
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
                            url: 'https://github.com/santiago-jv/reactjs-jenkins-pipeline.git'
                            //credentialsId: env.GITHUB_CREDENTIALS
                        ]
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
        stage('Deploy build to S3') {
             steps {
                withAWS(region: 'us-east-1', credentials: 'santiagojv-aws-credentials') {
                    s3Upload(path: '', 
                    bucket: env.S3_BUCKET,
                    file: 'dist/',
                    )
                }
            }
        }
    }
}