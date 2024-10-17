pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Mahagithub15/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
                sh 'docker build -t LoginWebApp-1:latest .' 
                sh 'docker tag samplewebapp Mahagithub15/LoginWebApp-1:latest'
                //sh 'docker tag samplewebapp Mahagithub15/LoginWebApp-1:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push Mahagithub15/LoginWebApp-1:latest'
        //  sh  'docker push Mahagithub15/LoginWebApp-1:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 Mahagithub15/LoginWebApp-1"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 Mahagithub15/LoginWebApp-1"
 
            }
        }
    }
	}
    
