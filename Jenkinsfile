pipeline {
    agent any
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
                            url: 'https://github.com/santiago-jv/reactjs-jenkins-pipeline.git']
                        ]
                ])
            }
        }
        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'NodeJS@16.0.0') {
                    sh 'npm i'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}