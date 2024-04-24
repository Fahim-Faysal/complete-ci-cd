pipeline {
    agent any
    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url: 'https://github.com/FFSiyam/practice-project.git'
            }
        }
        stage('dependencies install') {
            steps {
                sh 'sudo npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('docker file build') {
            steps {
                sh 'sudo docker build -t siyamapp .'
            }
    }
        

    }
}