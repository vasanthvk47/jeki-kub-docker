pipeline { 
    agent any 
    environment { 
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials' 
    } 
    stages { 
        stage('Clone Repo') { 
            steps { 
                git 'https://github.com/vasanthvk47/jeki-kub-docker.git' 
            } 
        } 
        stage('Build Docker Image') { 
            steps { 
                script { 
                    dockerImage = docker.build("vasanth4747/jenkins-k8s-demo") 
                } 
            } 
        } 
        stage('Push Docker Image') { 
            steps { 
                script { 
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) { 
                        dockerImage.push("latest") 
                    } 
                } 
            } 
        } 
        stage('Deploy to Kubernetes') { 
            steps { 
                sh 'kubectl apply -f k8s-deployment.yaml' 
            } 
        } 
    } 
} 
