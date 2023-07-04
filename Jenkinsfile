pipeline {
    agent any
    
    stages {
        stage('project build sender') {
            steps {
                script{
                    checkout scmGit(branches: [[name: '*/latest']], browser: github('https://github.com/secured-jenkins/Sender.git'), extensions: [], userRemoteConfigs: [[url: 'https://github.com/secured-jenkins/Sender.git']])
                }
            }
        }
        stage('dockerize sender'){
            steps{
                bat 'docker build --tag hasanalrimawi/sender-ci:latest .'
            }
        }
        stage('push image sender'){
            steps{
                bat 'docker push hasanalrimawi/sender-ci:latest'
            }
        }
         stage('project build receiver') {
            steps {
                script{
                    checkout scmGit(branches: [[name: '*/master']], browser: github('https://github.com/secured-jenkins/Receiver.git'), extensions: [], userRemoteConfigs: [[url: 'https://github.com/secured-jenkins/Receiver.git']])
                }
            }
        }
        stage('dockerize receiver'){
            steps{
                bat 'docker build --tag hasanalrimawi/receiver-ci:latest .'
            }
        }
        stage('push image receiver'){
            steps{
                bat 'docker push hasanalrimawi/receiver-ci:latest'
            }
        }
        stage('project build gateway') {
            steps {
                script{
                    checkout scmGit(branches: [[name: '*/master']], browser: github('https://github.com/secured-jenkins/gateway.git'), extensions: [], userRemoteConfigs: [[url: 'https://github.com/secured-jenkins/gateway.git']])
                }
            }
        }
        stage('dockerize gateway'){
            steps{
                bat 'docker build --tag hasanalrimawi/gateway-ci:latest .'
            }
        }
        stage('push image gateway'){
            steps{
                bat 'docker push hasanalrimawi/gateway-ci:latest'
            }
        }
        stage('project build eureka') {
            steps {
                script{
                    checkout scmGit(branches: [[name: '*/master']], browser: github('https://github.com/secured-jenkins/eureka.git'), extensions: [], userRemoteConfigs: [[url: 'https://github.com/secured-jenkins/eureka.git']])
                }
            }
        }
        stage('dockerize eureka'){
            steps{
                bat 'docker build --tag hasanalrimawi/eureka-ci:latest .'
            }
        }
        stage('push image eureka'){
            steps{
                bat 'docker push hasanalrimawi/eureka-ci:latest'
            }
        }
        stage('fire docker-compose'){
            steps{
                bat 'docker compose up'
            }
        }
    }
}
