pipeline {
    agent any
    // environment{
    //     DOCKERHUB_CREDENTIALS = credentials('docker-token')
    // }
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
                sh 'sudo docker build -t siyamapp:1.0 .'
            }
        }
        stage('push') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-token', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'sudo docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'sudo docker tag siyamapp:1.0 siyam05/siyamapp:1.0'
                    sh 'sudo docker push siyam05/siyamapp:1.0'
                    sh 'sudo docker logout'
            }
            
        }

    }
}
}
