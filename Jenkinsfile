pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                bat 'docker build -t nginxtest:latest .' 
                bat 'docker tag nginxtest idilassi/nginxtest:latest'
                bat 'docker tag nginxtest idilassi/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
         bat  'docker push idilassi/nginxtest:latest'
          bat  'docker push idilassi/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                bat "docker run -d -p 4030:80 nikhilnidhi/nginxtest"
 
            }
        }
