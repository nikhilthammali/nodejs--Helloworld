pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
    }
    
    stages {

        stage('SCM Checkout') {
            steps {
                git 'https://github.com/nikhilthammali/nodejs-Helloworld.git'
               }
           } 
       
        stage('Build docker image') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
               }
           }
       
        stage('login to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                sh 'echo \$DOCKERHUB_PASSWORD | docker login -u \$DOCKERHUB_USERNAME --password-stdin docker.io'
               } 
           }
   
        stage('Push image') {
            steps {
                sh 'docker tag ${DOCKER_IMAGE} ${DOCKER_IMAGE:TAG}'
                sh 'docker push ${DOCKER_IMAGE:TAG}'
               }
           }
       }
   }
}
post
   always {
        sh 'docker logout'
      }
