pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhubpwd'
        DOCKER_IMAGE_NAME = 'koushaliya/productfilter2'
    }


    stages {

            stage('gitclone') {

			steps {
				 
                 checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KoushaliyaSree/Productfilter.git']])
			}
		}



         stage('Build and Test') {
            steps {
                script {
                    // Install dependencies and build React application
                    sh 'npm install'
                   //sh 'npm run build'
                
                 }
             }
        }

         stage('Build Docker Image') {
             steps {
                 script {
             // Building Docker image
                     sh 'docker build -t koushaliya/productfilter2:latest .'

                 }
             }
         }


        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u koushaliya -p ${dockerhubpwd}'
                        sh 'docker push koushaliya/productfilter2:latest'
                    }
                    }
                }
            }   
        stage('Trigger CD Pipeline') {
            steps {
               build job:"ProductfilterCD", wait:true
             }
        }
       

       }
}
