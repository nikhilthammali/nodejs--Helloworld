pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
    }
    
    stages {
        stage('SCM Checkout') {
            steps {
                // Checkout the source code from the repository
                git 'https://github.com/nikhilthammali/nodejs-Helloworld.git'
                }
            }
        } 
       
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
       
        stage('Dockerhub lohin') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                  sh 'echo \$DOCKERHUB_PASSWORD | docker login -u \$DOCKERHUB_USERNAME --password-stdin docker.io'
       
        stage('Push Docker Image') {
            steps {
                  sh 'docker tag ${DOCKER_IMAGE} ${DOCKER_IMAGE:TAG}'
                  sh 'docker push ${DOCKER_IMAGE:TAG}'
                }
             }
          }       
      }
   }
}
