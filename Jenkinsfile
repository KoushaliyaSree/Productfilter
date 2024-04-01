pipeline {
    agent any

    environment{
        DOCKER_REGISTRY= 'koushaliya/product_filter'
    }

    tools {
        dockerTool 'docker'
    }

    stages {
        stage('Docker push'){
            steps {
                script {
                    docker.withRegistry('') {
                        def customImage= docker.build("$(DOCKER_REGISTRY):$(env.BUILD_ID)")

                        customImage.push()
                    }
                }
            }
        }

        

    }
}