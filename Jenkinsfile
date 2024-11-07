pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'lbg-hello-world-maven:latest' // Define a name for the Docker image
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git branch: 'main', url: 'https://github.com/John-D-Edmondson/lbg-hello-world-maven.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the current directory
                    def customImage = docker.build(DOCKER_IMAGE, '.')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container to execute the JAR file
                    sh "docker run --rm -v ${pwd()}/target:/app/target ${DOCKER_IMAGE}"
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
