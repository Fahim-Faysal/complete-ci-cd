pipeline {
    agent any
    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url:
            }
        }
        stage('dependencies install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
}