pipeline {
    agent any
    environment {
        registry = 'siyam05/siyamapp'
        registryCredential = 'docker-token'
    }
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
      
//using the plugin

        stage('build the image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":v$BUILD_NUMBER"
                }
            }
        }

        stage("upload image") {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("v$BUILD_NUMBER")
                        dockerImage.push("latest")
                    }
                }
            }
        }

        stage("remove unused image") {
            steps {
                sh "docker rmi $registry:v$BUILD_NUMBER"
            }
        }

 //Anothe Way of uploading

   // stage('docker file build') {
        //     steps {
        //         sh 'sudo docker build -t siyamapp:1.0 .'
        //     }
        // }

    //     stage('push') {
    //         steps{
    //             withCredentials([usernamePassword(credentialsId: 'docker-token', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
    //                 sh 'sudo docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
    //                 sh 'sudo docker tag siyamapp:1.0 siyam05/siyamapp:1.0'
    //                 sh 'sudo docker push siyam05/siyamapp:1.0'
    //                 sh 'sudo docker logout'
    //         }
            
    //     }

    // }
}
}
