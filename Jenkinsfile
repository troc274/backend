pipeline {
    agent any
    environment {
        IMAGE_NAME = "thonguyen2749/devops-hello-world:backend"  // Replace with your Docker image name
        DOCKERHUB_CREDENTIALS = credentials('8eb68f23-6497-4663-a47e-7f7045461567')  // Use your DockerHub credentials ID in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker rm -f java-app || true"
                    sh "docker rmi -f ${IMAGE_NAME} || true"
                    // Build the Docker image using the Dockerfile in the repository
                    docker.build("${IMAGE_NAME}", ".")
                }
            }
        }


        stage('Deploy and Run') {
            steps {
                script {
                    // Run the container to serve the application
                    sh "docker run -d --name java-app -p 4000:80 ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
        failure {
            echo 'The build or deployment failed.'
        }
    }
}
