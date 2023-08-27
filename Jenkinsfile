pipeline {
    agent any
    
    environment {
        GITHUB_CREDENTIALS = credentials('santiagojv-github-credentials')
        AWS_ACCESS_KEY_ID = credentials('santiagojv-aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('santiagojv-aws-secret-access-key')
        S3_BUCKET = 'santiagojv-deployments'
    }

    stages {
        stage("Show variables") {
            steps {
                sh 'echo $GITHUB_CREDENTIALS'
                sh 'echo $AWS_ACCESS_KEY_ID'
                sh 'echo $AWS_SECRET_ACCESS_KEY'
                sh 'echo $S3_BUCKET'
            }
        }
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
        stage('Upload build to S3') {
             steps {
                withAWS(region: 'us-east-1', credentials: 'aws-credentials') {
                    s3Upload(path: 'dist/**/*', includePathPattern: true, 
                    bucket: env.S3_BUCKET, workingDir: 'build/')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}