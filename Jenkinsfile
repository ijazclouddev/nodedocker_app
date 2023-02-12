pipeline {
    agent any
    tools { 
        maven 'Maven_Home' 
        jdk 'Java_Home' 
           }
           stages {
      stage('GIT checkout') {
           steps {
             
           //     git branch: 'main', url: 'https://github.com/ijazclouddev/CI-CD-Pipeline-with-Jenkins-deploy-tomcat'
                  git branch: 'docker-compose-nodejs-redis-app', url: 'https://github.com/ijazclouddev/nodedocker_app.git'
             
          }
        }
       /* stage('Compile') {
           steps {
               sh 'mvn clean test package'
            }
        }
        
        stage('Build') {
           steps {
               sh 'mvn clean install'
            }
        }*/
        
         stage('Docker Build'){
            steps{
                
             /*sh "docker build DockerUC1/ -t ijaz21/simpleexpressnodejs"*/
              sh "docker build . -t ijaz21/nodeexpredis"
              
            }
        }
        
        stage('Push to dockerHub'){
             steps{
                 withCredentials([string(credentialsId: 'dockerpassword', variable: 'Dockerpassword')]) {
                  sh "docker login -u ijaz21 -p ${Dockerpassword}"
                 
                 }
                 
                 sh "docker push ijaz21/nodeexpredis"
             }
         }
         
          stage('Docker Compose Execution'){
            steps{
                
             /*sh "docker build DockerUC1/ -t ijaz21/simpleexpressnodejs"*/
             sh "docker-compose down"
              sh "docker-compose up -d"
              
            }
        }
           }
}
