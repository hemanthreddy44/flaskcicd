pipeline {
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
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh " docker image push ${env.IMAGE_REPO}:${env.GIT_COMMIT}"
                  }
              }
         } 
          stage('deploy latesh image') {
              steps {
                  sh "deploy"
              }
         }
             }
        }
