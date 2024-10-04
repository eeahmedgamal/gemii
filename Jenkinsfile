pipeline 
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ahmedgamal01/repo/Gemii&HoassamFathalla&Nazmy-Image'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                   
                        sh 'docker push ahmedgamal01/repo/Gemii&HoassamFathalla&Nazmy-Image'
                    }
            }
        }
        stage('Pull Image on Another Agent') {
            agent { label 'remote-agent' } // Run on a different node/agent
            steps {
                script {
                    sh 'docker pull ahmedgamal01/repo/Gemii&HoassamFathalla&Nazmy-Image'
                }
            }
        }
        stage('Run the Image') {
            steps {
                script {
                    sh 'docker run -d -p 8080:8080 ahmedgamal01/repo/Gemii&HoassamFathalla&Nazmy-Image'
                }
            }
        }
        stage('Check Connectivity') {
            steps {
                script {
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

