pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'df54a111-3c2f-4ba3-a6d5-306a5e38cdfd' // Replace with your Docker Hub credentials ID in Jenkins
        DOCKER_REPO = "gowtham47/nginx" // Replace with your Docker Hub username and image name
        DOCKER_TAG = "latest" // Replace with the desired image tag
        GIT_REPO_URL = "https://github.com/Gowtham-Attili/mini-project.git" // Replace with your GitHub repository URL
        DOCKERFILE_PATH = "Dockerfile" // Replace with the path to your Dockerfile in the repository
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: GIT_REPO_URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage // Define dockerImage variable in this scope
                    dockerImage = docker.build("${DOCKER_REPO}:${DOCKER_TAG}", "-f ${DOCKERFILE_PATH} .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    def dockerImage // Define dockerImage variable in this scope
                    dockerImage = docker.image("${DOCKER_REPO}:${DOCKER_TAG}") // Retrieve the existing Docker image
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        dockerImage.push()
                    }
                }
            }
        }
  	    stage('Deploy on k8s') {
  	        steps{
                withKubeConfig([credentialsId: 'newk8s']) {
                    powershell """(kubectl apply -f D:/try/deploy.yml)"""
                    powershell """(kubectl get deployments)"""
                    powershell """(kubectl get services)"""
                    
  	            }
            }
  	    }

}
}
