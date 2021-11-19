pipeline {
     agent any
environment {
    IMAGE_REPO = "hemanthhr/flaskhello"
    // Instead of hemanthhr, use your git username
}     
     stages {
         stage('Build Docker Image') {
              steps {

                  sh " docker image build -t  ${env.IMAGE_REPO}:${env.GIT_COMMIT} ."
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh " docker image push ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
                      sh " aws s3 ls"
                      sh "docker image tag ${env.IMAGE_REPO}:${env.GIT_COMMIT} public.ecr.aws/c4b1v8n7/hemanthflaskapp:latest"
                      sh "docker push public.ecr.aws/c4b1v8n7/hemanthflaskapp:latest"
                  }
              }
         }  
             }
        }
