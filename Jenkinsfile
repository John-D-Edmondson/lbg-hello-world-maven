pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-docker-image:latest' // Define a name for the Docker image
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git branch: 'main', url: 'https://your-repo-url.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    def customImage = docker.build(DOCKER_IMAGE, '.')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container to produce the JAR file
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'java -jar /app/lbg-hello-world-maven.jar'
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                // Archive the JAR file
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Pipeline succeeded'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
