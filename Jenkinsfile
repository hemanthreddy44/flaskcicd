pipeline {
     agent any
environment {
    IMAGE_REPO = "hemanthreddy44/argotest"
    GIT_CREDS = credentials('github')
    HELM_GIT_REPO_URL = "github.com/hemanthreddy44/samplenginxhelm.git"
    GIT_REPO_EMAIL = 'hemanthhr1344@gmail.com'
    GIT_REPO_BRANCH = "master"
    // Instead of hemanthhr, use your git username
}     
     stages {
         stage('Build Docker Image') {
              steps {
                  sh "ls"
                  sh " docker image build -t  ${env.IMAGE_REPO}:${env.GIT_COMMIT} ."
              }
         }
         stage('deploy latesh image') {
              steps {
                  sh "docker stop demo"
                  sh "docker rm demo "
                  sh "docker run --restart always --name demo -p 5000:5000 -d ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
              }
         }
        
             
         stage('Push Docker Image') {
              steps {
        // Login to DockerHub
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
          sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
        }
          sh "docker push ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
              }
         } 
          stage('update image tag')
          {
               steps{
                sh "git clone https://${env.HELM_GIT_REPO_URL}"
                sh "git config --global user.email ${env.GIT_REPO_EMAIL}"
               }
          }
     }
}
