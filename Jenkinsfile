pipeline {
     agent any
environment {
    IMAGE_REPO = "hemanthreddy44/argotest"
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
             
         stage('Push Docker Image')
         environment {
        DOCKERHUB_CREDS = credentials('dockerhub')
             }
              steps {
                     {
                     sh "echo ${env.GIT_COMMIT}"
                     sh "docker push ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
                     sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW && docker image push ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
                  }

          stage('deploy latesh images') {
              steps {
                  sh "deploy"
              }
         }
             }
        
}
