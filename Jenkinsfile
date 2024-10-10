pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t ahmedgamal01/gemii-hoassamfathalla-nazmy-image .'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([ credentialsId: 'docker-hub-creds', url: 'https://index.docker.io/v1/' ]) {
                        // Push the built image to Docker Hub
                        sh 'docker push ahmedgamal01/gemii-hoassamfathalla-nazmy-image'
                    }
                }
            }
        }
        stage('Pull Image on Another Agent') {
            agent { label 'gemii-2' } // Run on a different node/agent
            steps {
                script {
                    // Pull the image from Docker Hub
                    sh 'docker pull ahmedgamal01/gemii-hoassamfathalla-nazmy-image'
                }
            }
        }
        stage('Run the Image') {
            agent { label 'gemii-2' }
            steps {
                script {
                    // Run the Docker image on port 8080
                    sh 'docker run -d -p 8080:8080 ahmedgamal01/gemii-hoassamfathalla-nazmy-image'
                }
            }
        }
        stage('Check Connectivity') {
            agent { label 'gemii-2' } // Ensure curl runs on the same agent where the container is running
            steps {
                script {
                    // Check if the website is accessible
                    sh 'curl http://localhost:8080'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}























































