pipeline{
    agent any
    
    tools {
        maven 'Maven 3.9.9'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/John-D-Edmondson/lbg-hello-world-maven.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage ('Test') {
            steps {
                sh 'mvn -Dmaven.compile.skip test'
            }
        }
        stage ('Package') {
            steps {
                sh 'mvn -Dmaven.test.skip -Dmaven.compile.skip package'
            }
        }
    }
    
    
    
    
    
    
}
