pipeline {
     agent any
     stages {
         stage('Build') {
              steps {
                  sh 'echo Building...'
              }
         }

         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t flaskhello .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh "docker tag flaskhello hemanthhr/flaskhello"
                      sh 'docker push hemanthhr/flaskhello'
                  }
              }
         }  
             }
        }
