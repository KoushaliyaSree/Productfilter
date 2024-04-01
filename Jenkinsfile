pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'https://index.docker.io/v1//' // Docker Hub URL or your private registry URL
        DOCKER_CREDENTIALS_ID = 'koushaliya/product_filter' // Jenkins credentials ID for Docker Hub or your private registry
        REACT_APP_NAME = 'Productfilter'        
        // TOMCAT_URL = 'http://localhost:8081' // URL of the Tomcat server
        // TOMCAT_USER = 'admin' // Tomcat username with manager role
        // TOMCAT_PASSWORD = 'admin' // Password for the Tomcat user
    }

    stages {

         stage('Build and Test') {
            steps {
                script {
                    // Install dependencies and build React application
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Building Docker image
                    //def customImage = docker.build("${DOCKER_REGISTRY}/your-image-name:${env.BUILD_ID}")
                    def customImage = docker.build("${DOCKER_REGISTRY}/${REACT_APP_NAME}:${env.BUILD_ID}")

                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Pushing Docker image to registry
                    docker.withRegistry("${DOCKER_REGISTRY}", "${DOCKER_CREDENTIALS_ID}") {
                        customImage.push()
                    }
                }
            }
        }

        // stage('Deploy to Tomcat') {
        //     steps {
        //         script {
        //             // Deploying Docker image to Tomcat
        //             withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASSWORD')]) {
        //                 sh "curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} -T target/your-war-file.war ${TOMCAT_URL}/manager/text/deploy?path=/your-app-context"
        //             }
        //         }
        //     }
        // }
    }
}
