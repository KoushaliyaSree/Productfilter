pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhubpwd'
        DOCKER_IMAGE_NAME = 'koushaliya/product_filter'
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
                     sh 'docker build -t productfilter .'

                 }
             }
         }

       
       

       }
}
