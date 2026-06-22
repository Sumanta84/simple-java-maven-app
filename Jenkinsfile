pipeline {
    agent {
        docker {
            image 'maven:3.9.9-eclipse-temurin-21-alpine'
            args '-v maven-repo:/root/.m2 -u root:root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        APP_NAME = 'sample-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'git@github.com:devopsdiscipuli/simple-java-maven-app.git',
                    credentialsId: 'u6-java-project'
            }
        }
        stage('Install Docker CLI') {
            steps {
                sh '''
                    apk update
                    apk add --no-cache docker-cli
                    docker --version
                '''
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sample-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                // Stop and remove old container if exists
                sh '''
                    docker stop sample-app-container || true
                    docker rm sample-app-container || true
                    docker run -d --name sample-app-container -p 8080:8080 sample-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo "${APP_NAME} pipeline completed successfully"
        }
        failure {
            echo "${APP_NAME} pipeline failed. Check logs"
        }
        
    }
           
}