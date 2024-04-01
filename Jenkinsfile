pipeline {
    agent any

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
        //             // Building Docker image
        //             //def customImage = docker.build("${DOCKER_REGISTRY}/your-image-name:${env.BUILD_ID}")
        //             //def customImage = docker.build("${DOCKER_REGISTRY}/${Productfilter}:${env.BUILD_ID}")
                     sh 'docker build -t productfilter .'

                 }
             }
         }

        // stage('Push Docker Image') {
        //     steps {
        //         script {
        //             // Pushing Docker image to registry
        //             docker.withRegistry("${DOCKER_REGISTRY}", "${DOCKER_CREDENTIALS_ID}") {
        //                 customImage.push()
        //             }
        //         }
        //     }
        // }

        // stage('Deploy to Tomcat') {
        //     steps {
        //         script {
        //             // Deploying Docker image to Tomcat
        //             withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASSWORD')]) {
        //                 sh "curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} -T target/your-war-file.war ${TOMCAT_URL}/manager/text/deploy?path=/your-app-context"
        //             }
        //         }
        //     }
         //}
    }
}
