pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
     environment {     
         DOCKERHUB_CREDENTIALS= credentials('docker-hub')     
       } 

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    stage('Build Docker Image') {         
      steps{                
	sh 'docker build -t jyotiranswain/wabapp2:$BUILD_NUMBER .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{                            
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh 'docker push jyotiranswain/wabapp2:$BUILD_NUMBER'                 
  echo 'Push Image Completed'       
      }           
    }      
  } //stages 
  post{
    always {  
      sh 'docker logout'           
    }      

    }
    stage('Build'){
            steps {
                sh 'ssh root@13.233.92.158 "docker run -d --name=webapp1 -p 8282:8080 jyotiranswain/wabapp2:$BUILD_NUMBER"'
            }
            
        }
}
